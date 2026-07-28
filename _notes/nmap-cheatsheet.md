---
title: "Nmap Cheat Sheet"
description: "The scan patterns I use most often during CTF enumeration, from quick discovery to targeted service scripts."
date: 2026-06-03
area: "Enumeration"
tags: ["nmap", "recon", "tcp", "udp"]
---

## Quick TCP Pass

```bash
nmap -p- --min-rate 5000 -oN scans/all-tcp.txt TARGET
```

## Service Detection

```bash
nmap -sCV -p PORTS -oN scans/services.txt TARGET
```

## UDP Starter

```bash
sudo nmap -sU --top-ports 30 -oN scans/top-udp.txt TARGET
```

## Useful Script Categories

```bash
nmap --script vuln -p PORTS TARGET
nmap --script smb-enum-shares,smb-enum-users -p445 TARGET
nmap --script http-title,http-enum -p80,443 TARGET
```

## Habit

Save scans into a `scans/` folder. Future me should never need to rerun basic enumeration just to remember what was open.
