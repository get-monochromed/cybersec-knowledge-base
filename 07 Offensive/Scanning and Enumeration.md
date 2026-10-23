---
title: Scanning and Enumeration
aliases: [Enumeration, Port Scanning, Nmap, Service Discovery]
category: offensive
tags: [offensive/recon, tools]
status: solid
up: "[[Offensive MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Scanning and Enumeration

## Summary

Turning a host list into an attack plan: which ports are open, what software and version, what users and shares exist, what is misconfigured. Enumeration is where penetration tests are actually won — exploitation is usually the easy part once the surface is known.

## Host discovery

`nmap -sn`, ARP scan on local subnets, ICMP/TCP probes. Firewalls often block ICMP — scan a few common ports instead. Cloud environments: check metadata and public IP ranges.

## Port scanning essentials

```bash
nmap -sS -p- --min-rate 1000 -oA full <target>          # all TCP ports, fast
nmap -sU --top-ports 100 <target>                       # common UDP (DNS, SNMP, NTP)
nmap -sV -sC -p 22,80,443,445 <target>                  # versions + default scripts
nmap --script vuln -p 80,443 <target>                   # noisy vuln checks
```

Port states: **open**, **closed** (RST), **filtered** (no response/dropped). `-sS` (SYN) requires root; `-sT` (connect) works without.

## Enumeration by service

| Service | What to extract |
|---|---|
| SMB (445) | shares, null sessions, signing, users (`smbclient`, `enum4linux-ng`, `netexec`) |
| LDAP/AD (389/636) | users, groups, password policy, SPNs (`ldapsearch`, BloodHound later) |
| HTTP(S) | vhosts, directories, headers, frameworks, default pages (`ffuf`, `gobuster`, `nikto`) |
| DNS (53) | zone transfer, subdomains, mail records |
| SNMP (161) | community strings, interface and process data |
| NFS (2049) | exported shares (`showmount -e`) |
| SSH (22) | banner, auth methods, weak algorithms |
| Databases | version, default creds, exposed management (3306, 5432, 1433, 27017) |

## Vulnerability identification

- `nuclei` (template-based, fast, CVEs + misconfigs), `nikto` (web), OpenVAS/Nessus (authenticated scans), `searchsploit` for known exploits.
- Always verify — scanners produce false positives, and "the scanner said" is not a finding.
- Credential attacks belong here too: `hydra`, `netexec` spraying ([[Password Attacks]]) — with rate limits and lockout awareness.

## Detection and defence

Scans are noisy: firewall/IDS logs show sequential port touches, `nmap` user-agents in web logs, 404 storms from content discovery. Defenders should alert on internal scanning ([[Worm|worm behaviour]]) and on internet-wide scanning that reaches exposed admin ports ([[Attack Surface]]).

## Related

- [[Reconnaissance]]
- [[Exploitation]]
- [[Security Tools]]
- [[Vulnerability Management]]
- [[Offensive MOC]]
