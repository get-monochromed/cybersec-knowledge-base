---
title: Ports and Protocols
aliases: [Common Ports, Port Reference]
category: reference
tags: [reference, network]
status: solid
up: "[[Reference MOC]]"
created: 2026-10-23
updated: 2026-10-24
sources: []
---

# Ports and Protocols

## Must-know

| Port | Protocol | Notes |
|---|---|---|
| 20/21 | FTP | plaintext credentials; use SFTP |
| 22 | SSH | admin access; brute-force target |
| 23 | Telnet | plaintext; should not exist |
| 25 | SMTP | mail transfer; open relay risk |
| 53 | DNS (UDP/TCP) | tunnelling, amplification |
| 67/68 | DHCP | rogue DHCP, starvation |
| 80 | HTTP | redirect to 443; HSTS |
| 123 | NTP | amplification; time skew breaks logs |
| 135/139/445 | RPC/NetBIOS/SMB | **445 = ransomware's favourite**; [[EternalBlue]] and [[WannaCry]] live here |
| 143/993/995 | IMAP/IMAPS/POP3S | legacy auth bypasses in cloud |
| 161/162 | SNMP | v1/v2c community strings = plaintext |
| 389/636 | LDAP/LDAPS | AD enumeration |
| 443 | HTTPS | TLS |
| 1433 | MSSQL | exposed DB, `xp_cmdshell` |
| 1521 | Oracle DB | |
| 2049 | NFS | exports, no auth by default |
| 3306 | MySQL | |
| 3389 | RDP | **top ransomware entry point if exposed**; [[BlueKeep]] (CVE-2019-0708) is pre-auth RCE |
| 5432 | PostgreSQL | |
| 5900–5903 | VNC | often unauthenticated |
| 5985/5986 | WinRM | remote management |
| 6379 | Redis | unauthenticated by default |
| 8080/8443 | HTTP(S) alt | proxies, admin panels |
| 9200 | Elasticsearch | open clusters, data theft |
| 11211 | Memcached | 50,000× amplification |
| 27017 | MongoDB | open by default historically |

## Notes

- A port open ≠ service reachable; check both TCP and UDP (`nmap -sU`).
- Management ports (22, 3389, 5985, 8080, 9200) on the internet are an emergency, not a finding to schedule ([[Attack Surface]]).
- Egress restrictions should allow-list destinations, not just ports — attackers use 443.
- `nmap-services` and IANA registry for the full list; `ss -tulpn` / `netstat -ano` to see local listeners.

## Related

- [[Scanning and Enumeration]]
- [[Firewall]]
- [[Network Security]]
- [[Reference MOC]]
