---
title: Business Continuity and Disaster Recovery
aliases: [BCDR, BCP, DR, Business Continuity]
category: grc
tags: [grc/resilience, exam]
status: solid
up: "[[GRC MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Business Continuity and Disaster Recovery

## Summary

Keeping the business running through disruption, and restoring it afterwards. DR is the technical recovery of systems; **BC** is the wider organisational capability — people, premises, suppliers, communications. Ransomware made BCDR a security topic rather than an afterthought.

## Core inputs

- **BIA (Business Impact Analysis)** — for each process: maximum tolerable downtime, financial/regulatory impact, dependencies.
- **RTO** — target time to restore a service.
- **RPO** — acceptable data loss window (drives [[Backup and Recovery]] design).
- **MTD/MAO** — maximum tolerable downtime / outage before unacceptable harm.

## Strategy

Rank processes by criticality, then choose per tier:

- **Hot site / active-active** — near-zero RTO, expensive.
- **Warm site** — infrastructure ready, data restored on demand.
- **Cold site / rebuild** — cheap, slow (hours to days).
- **Cloud DR** — pilot light, backup-and-restore, multi-region.
- **Manual workarounds** — for processes that can survive on paper for a day.

Keep RTO/RPO *realistic and tested*; the number in the plan is a claim until exercised.

## Plans

Crisis management (who declares, who decides, comms), IT DR runbooks (ordered recovery steps, dependency map), facilities, supplier contacts, and **manual copies** of the plan — you cannot look up the DR plan on the systems that are down.

## Testing

Tabletop → simulation → partial failover → full failover. Vary scenarios: ransomware, cloud region outage, key-person loss, supplier failure. Record actual RTO vs target; fix the gap.

## Security intersection

- Ransomware resilience needs immutable/offline backups and a clean-room restore ([[Ransomware]]).
- DR environments are often less hardened — an attacker who waits for failover gets a softer target.
- Regulatory expectations: [[ISO 27001]] A.5.29/8.13, [[NIST CSF]] Recover, sector rules (RBI, SEBI, DORA in the EU).

## Related

- [[Backup and Recovery]]
- [[Incident Response]]
- [[Risk Management]]
- [[GRC MOC]]
