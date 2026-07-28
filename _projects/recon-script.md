---
title: "Recon Script"
description: "A planned Bash/Python helper that creates folders, runs baseline scans, and stores output consistently for CTF boxes."
date: 2026-06-07
status: "Idea"
tags: ["automation", "nmap", "bash", "python"]
---

## Problem

I repeat the same setup steps on every target. A small helper can reduce mistakes and keep output consistent.

## Planned Features

- Create `scans/`, `loot/`, and `screenshots/`.
- Run fast TCP discovery.
- Parse open ports into a service scan.
- Save commands into a session log.

## First Version

Start boring: one target, one workspace, clear output. Add options only after the basic flow is reliable.
