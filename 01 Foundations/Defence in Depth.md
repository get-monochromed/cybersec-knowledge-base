---
title: Defence in Depth
aliases: [Layered Defence, Layered Security, DiD]
category: foundation
tags: [foundation/core, design]
status: solid
up: "[[Foundations MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Defence in Depth

## Summary

Assume every individual control will fail, and arrange controls so that a single failure does not become a breach. The point is not "many controls" but *independent* controls at *different* layers, so the same bypass cannot defeat two of them.

## The layers

1. **Physical** — site access control, locks, tamper-evident hardware, device encryption for stolen laptops.
2. **Network** — [[Firewall]], [[Network Segmentation]], [[VPN]]/ZTNA, [[IDS and IPS]].
3. **Perimeter / edge** — [[WAF]], DDoS scrubbing, email filtering ([[Email Security]]).
4. **Endpoint** — [[Endpoint Protection]] (AV/EDR), [[Hardening]], application allow-listing.
5. **Identity** — MFA, [[Access Control Models]], privileged access management ([[Authentication, Authorization and Accounting]]).
6. **Application** — input validation, secure coding ([[Application Security]]), [[Web Application Security]].
7. **Data** — encryption at rest and in transit ([[TLS]], [[Key Management]]), classification, DLP, [[Backup and Recovery]].
8. **People and process** — [[Security Awareness Training]], [[Incident Response]], [[Security Policy]].

## Independence is the whole trick

Layering three signature-based AV products is one layer, not three. Good depth means *different failure modes*:

- Phishing email → mail filter (preventive), user report button (detective), EDR on the endpoint (preventive/detective), EDR blocks the payload's behaviour, egress filtering stops C2, segmentation stops [[Lateral Movement]], backups blunt [[Ransomware]].
- Attacker steals a session cookie → TLS still protects other traffic, MFA blocks re-auth without the second factor, anomaly detection in [[SIEM]] flags the new device.

## Attack requires crossing every layer

Frameworks model this explicitly: the [[MITRE ATT&CK]] matrix is essentially a defence-in-depth map of the kill chain — initial access, execution, persistence, privilege escalation, credential access, discovery, lateral movement, collection, exfiltration, impact. Failure at one tactic should be detected or blocked before the next.

## Trade-offs

- Cost, alert volume, and operational drag. Each layer produces noise and maintenance.
- Layered controls that overlap identically add cost without resilience.
- "Castle-and-moat" (hard perimeter, soft interior) is depth in name only — once inside, nothing stops movement. Fix with [[Zero Trust Architecture]] and segmentation.

## How to test it

Red teaming and purple teaming: pick a realistic attack path, see how many layers actually alert or block ([[Purple Teaming]], [[Red Teaming]]). Assumed coverage is the most common audit finding.

## Related

- [[Security Principles]]
- [[Security Controls]]
- [[Network Segmentation]]
- [[Zero Trust Architecture]]
- [[MITRE ATT&CK]]
- [[Foundations MOC]]
