---
title: Security Controls
aliases: [Controls, Countermeasures, Safeguards]
category: foundation
tags: [foundation/core, grc, exam]
status: solid
up: "[[Foundations MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Security Controls

## Summary

A control is any safeguard that changes the likelihood or impact of a threat. Nearly every certification, audit and risk register is really an argument about which controls exist, whether they work, and whether they are evidenced.

## By function

| Type | Purpose | Examples |
|---|---|---|
| **Preventive** | Stop the event | [[Firewall]], [[WAF]], MFA, [[Access Control Models]], patching |
| **Detective** | Discover it happened or is happening | [[IDS and IPS]], [[SIEM]], file integrity monitoring, [[Threat Hunting]] |
| **Corrective** | Reduce impact after the event | [[Backup and Recovery]], [[Incident Response]], failover |
| **Deterrent** | Discourage the attempt | Warning banners, [[Honeypot]], visible CCTV, legal notices |
| **Compensating** | Alternative when the primary control is impossible | Network segmentation because a legacy host cannot be patched |
| **Directive** | Tell people what to do | [[Security Policy]], [[Security Awareness Training]] |

## By nature

- **Technical / logical** — implemented in software or config (firewall rules, EDR).
- **Administrative / managerial** — process and people (policies, background checks, training).
- **Physical** — locks, doors, badge readers, UPS. Physical access usually defeats everything else (see [[Post Exploitation]] — evil maid, USB drops).

## By implementation

Preventive/detective/corrective is *what it does*; technical/admin/physical is *how it is delivered*. A control is described with both: "detective technical control — EDR telemetry to [[SIEM]]".

## Judging controls

- **Coverage** — which assets, which [[Attack Surface]]?
- **Effectiveness** — tested, or assumed? Untested controls are marketing.
- **Cost vs risk reduction** — see [[Risk Management]].
- **Bypass resistance** — single point of failure? Can an admin disable it silently?
- **Evidence** — auditors want logs or screenshots, not assurances ([[Compliance Audit]]).

## Control frameworks

[[CIS Controls]] (prioritised, practical), [[NIST CSF]] (function-level outcomes), [[ISO 27001]] Annex A (certifiable management system), [[NIST 800-53]] (catalogue for US federal, widely borrowed), [[PCI DSS]] (payment-specific).

## Related

- [[Defence in Depth]]
- [[Risk Management]]
- [[Security Principles]]
- [[CIS Controls]]
- [[Foundations MOC]]
