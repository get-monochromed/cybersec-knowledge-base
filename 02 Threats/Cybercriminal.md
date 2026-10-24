---
title: Cybercriminal
aliases: [Criminal Group, Organised Crime, Ransomware Group]
category: actor
tags: [actor/financial, ransomware]
status: solid
up: "[[Threats MOC]]"
created: 2026-10-23
updated: 2026-10-24
sources: []
---

# Cybercriminal

## Summary

Financially motivated, professionally organised actor. Today's dominant threat: the ecosystem is a supply chain of specialists — initial access brokers, malware developers, ransomware operators, negotiators, money launderers — often communicating only through forums and escrow.

## Motivation

Revenue with low risk of prosecution. Return on investment drives target selection: who pays fastest, who has insurance, who has no backups.

## Capability

- Medium to very high: bought or rented tooling, professional OPSEC, helpdesks for affiliates.
- **Ransomware-as-a-Service (RaaS)**: developers sell or rent the encryptor; affiliates do the intrusion and keep a cut. Lowers the skill barrier drastically.
- **Initial Access Brokers (IABs)** sell footholds (VPN creds, RDP, webshells) on dark-web markets — mapped as the initial access tactic in [[MITRE ATT&CK]].
- **Botnet-as-a-service**: rent an existing infected base for spam, trojan, ransomware or DDoS delivery instead of building one; [[Kelihos]] sold exactly this. Distribution is the product.
- **Double/triple extortion**: encrypt + exfiltrate + threaten to leak + DDoS + harass customers.

## Typical TTPs

- [[Phishing]] and [[Business Email Compromise]]; credential stuffing; [[VPN]] appliance vulnerabilities; exposed RDP.
- [[Ransomware]] deployment after [[Lateral Movement]] and backup destruction.
- [[Privilege Escalation]] to domain admin; data theft before encryption.
- Use of legitimate tools ([[Living off the Land]]) to evade signature detection.

## Defensive focus

- Availability and recovery: tested offline [[Backup and Recovery]] (3-2-1), fast restore, immutable backups.
- Identity: MFA, no exposed RDP/VPN without hardening, privileged access management.
- Detection of *behaviour*, not just files: [[Endpoint Protection|EDR]], [[SIEM]] correlation, [[Threat Hunting]] for known RaaS TTPs.
- Assume exfiltration happens before encryption — protect and monitor egress.
- Incident response retainer and a tested playbook; negotiation is a business decision, not a technical one.

## Related

- [[Ransomware]]
- [[Advanced Persistent Threat]]
- [[Threat Actor]]
- [[Business Email Compromise]]
- [[Backup and Recovery]]
- [[Kelihos]]
- [[Botnet]]
- [[Threats MOC]]
