---
title: Firewall
aliases: [Network Firewall, NGFW, Packet Filter]
category: defence
tags: [defence/network, perimeter]
status: solid
up: "[[Defences MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Firewall

## Summary

Enforces a network policy at a choke point: which traffic is allowed between zones. Everything else is policy design — most breaches attributed to "firewall failure" are actually "permit any any" or nobody owning the rulebase.

## Generations

1. **Packet filter** (stateless) — inspect 5-tuple per packet; simple, no connection awareness.
2. **Stateful inspection** — tracks connection state, allows return traffic automatically, understands TCP flags.
3. **Application/proxy** — terminates and inspects a protocol (HTTP, SMTP) at L7.
4. **NGFW** — stateful + application identification + IPS + TLS inspection + user identity + threat feeds.
5. **Cloud-native** — security groups, NACLs, NSGs, firewall policies in IAM; west-east control matters more than north-south.
6. **Host firewall** — `iptables`/`nftables`, Windows Defender Firewall, `ufw`; last line of defence and often the strongest.

## Design principles

- **Default deny inbound, allow-list egress** — egress control is underrated and blocks C2/exfiltration.
- **Zone model**: internet, DMZ, internal, management, IoT/OT. Traffic between zones is explicit ([[Network Segmentation]]).
- **Rules have owners and expiry.** Orphaned rules are an audit finding and an attack path.
- **Least privilege for rules** — no `any/any`, no broad management access from the internet.
- **Log denies and allows for sensitive flows** into the [[SIEM]]; firewall logs are primary incident evidence.

## Failure modes

- Rule sprawl (thousands of shadowed rules) and "temporary" exceptions from 2019.
- Management plane exposed to the internet, or an unpatched appliance (VPN/firewall CVEs are a top initial-access vector).
- No egress control, so malware calls home freely.
- Trusting the internal network — see [[Zero Trust Architecture]].
- Assuming the firewall sees encrypted traffic; without TLS inspection, NGFW is mostly metadata.

## Related

- [[IDS and IPS]]
- [[WAF]]
- [[Network Segmentation]]
- [[Zero Trust Architecture]]
- [[Defences MOC]]
