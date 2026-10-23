---
title: Network Security
aliases: [Network Security Domain]
category: domain
tags: [domain/network]
status: solid
up: "[[Domains MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Network Security

## Summary

Protecting data in motion and controlling reachability. In a zero-trust world the network is no longer the perimeter, but it remains where you contain damage — segmentation and monitoring are still the strongest levers.

## Threat model

- Interception: [[Man-in-the-Middle (MITM)]], [[ARP Spoofing]], [[DNS Attacks]], [[Wireless Attacks]].
- Exposure: open services and management interfaces ([[Attack Surface]]).
- Movement: flat networks enabling [[Lateral Movement]] and [[Worm|worms]].
- Availability: [[Denial of Service (DoS)]].
- Perimeter devices as entry points: unpatched [[VPN]]/firewall appliances.

## Controls

| Layer | Controls |
|---|---|
| Perimeter | [[Firewall]], DDoS protection, [[VPN]]/ZTNA, egress filtering |
| Internal | [[Network Segmentation]], private VLANs, 802.1X |
| Detection | [[IDS and IPS]], flow analysis (NetFlow/IPFIX), DNS logging, [[Honeypot]] |
| Confidentiality | [[TLS]] everywhere, IPsec for site links, encrypted DNS |
| Access | NAC, ZTNA, jump hosts/PAWs for admin |

## Protocol-level hygiene

- Disable legacy: SMBv1, LLMNR, NBT-NS, Telnet, FTP, SNMPv1/v2c, SSLv3/TLS1.0.
- Prefer IPv6-aware controls — dual-stack often bypasses IPv4-only firewall rules.
- Harden BGP/RPKI where you operate routing; watch for BGP hijacks.
- Encrypt management planes (SSH, HTTPS, SNMPv3).

## Monitoring priorities

1. Egress to rare destinations (C2, exfiltration).
2. Internal scanning / fan-out ([[Worm]]).
3. Authentication to network devices (TACACS+/RADIUS logs).
4. DNS anomalies (DGA, tunnelling).

## Related

- [[Firewall]]
- [[Network Segmentation]]
- [[Zero Trust Architecture]]
- [[TLS]]
- [[Domains MOC]]
