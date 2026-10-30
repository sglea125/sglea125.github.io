---
title: "AD Home Lab Part 1: Architecture & Planning"
date: 2026-10-30 00:00:00 -0700
categories: [Home Lab, Active Directory]
tags: [active-directory, hyper-v, windows-server, networking]
---

## Goal
Build a small enterprise Windows environment to practice the day-to-day
work of a help desk / sysadmin role: user management, Group Policy,
DNS/DHCP and ticket-driven troubleshooting.

## Lab Design

| Component | Details |
|---|---|
| Hypervisor | Hyper-V on Windows 11 Pro (Ryzen 7 3700X, 16 GB RAM) |
| Network | Internal switch + NAT, 192.168.50.0/24 |
| DC01 | Windows Server 2025: AD DS, DNS, DHCP (192.168.50.10) |
| CLIENT01 | Windows 11 Enterprise, domain-joined (DHCP) |
| Domain | corp.internal |

## Design Decisions
- **Hyper-V over VirtualBox**: native to Windows Pro, works alongside WSL2,
  and is widely used in enterprise environments.
- **`.internal` domain**: officially reserved for private networks, which avoids
  the mDNS conflicts that `.local` can cause.
- **NAT network**: isolates the lab from my home network while still
  allowing internet access for updates.

## Problems & Fixes
- **"The requested operation requires elevation"** when enabling Hyper-V:
  PowerShell wasn't running as Administrator. Relaunched with
  *Run as administrator* and it worked.

## What's Next
Part 2: promoting DC01 to a domain controller and configuring DNS and DHCP.
