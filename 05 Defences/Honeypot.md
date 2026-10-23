---
title: Honeypot
aliases: [Honeypot, Honeynet, Deception, Canary Token]
category: defence
tags: [defence/detection, deception]
status: developing
up: "[[Defences MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Honeypot

## Summary

A decoy system, service, account or file whose only purpose is to be attacked. Any interaction is high-fidelity — legitimate users have no reason to touch it, so false positives approach zero.

## Types

- **Low-interaction** — emulated services (Dionaea, Cowrie for SSH). Cheap, limited intelligence.
- **High-interaction** — real OS in a controlled network (honeynet). Rich intelligence, higher risk.
- **Honeytokens / canary tokens** — fake credentials, AWS keys, documents, database records, DNS names; alert on use.
- **Honey accounts** — a privileged-looking account that is never used legitimately ([[Lateral Movement]] detection).
- **Canary files** — tripwire for [[Ransomware]] encryption.
- **Deception platforms** — commercial: fake shares, endpoints, AD objects at scale.

## Uses

- Early warning of lateral movement and recon.
- Attacker TTP collection (malware samples, C2, tools) for [[Threat Intelligence]].
- Ransomware detection (canary file modified → isolate immediately).
- Distraction: waste attacker time in a decoy network.

## Risks and limits

- Legal/ethical: do not entrap, do not collect more PII than necessary; keep honeypots clearly separated.
- Containment failure: a high-interaction honeypot that escapes becomes a foothold.
- Attackers can detect honeypots (VM artefacts, uptime, traffic patterns).
- Requires someone to monitor the alerts — otherwise it is decoration.

## Implementation notes

- Put honeypots in a dedicated isolated VLAN with egress to a monitoring collector only ([[Network Segmentation]]).
- Alert to [[SIEM]] with high severity; route to an on-call playbook.
- Refresh decoy content so it looks used.

## Related

- [[IDS and IPS]]
- [[Threat Hunting]]
- [[Ransomware]]
- [[Network Segmentation]]
- [[Defences MOC]]
