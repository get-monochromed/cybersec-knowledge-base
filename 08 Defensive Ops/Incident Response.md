---
title: Incident Response
aliases: [IR, Incident Handling, NIST 800-61, PICERL]
category: defensive
tags: [defensive/ir, exam]
status: solid
up: "[[Defensive Ops MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: ["NIST SP 800-61r3", "SANS PICERL"]
---

# Incident Response

## Summary

The process for handling a confirmed or suspected security incident: contain the damage, remove the attacker, restore service, learn something. Decided in advance (playbooks, contacts, authority) or improvised under pressure — the difference is measured in hours of downtime.

## Phases (NIST / SANS)

1. **Preparation** — playbooks, contacts, tooling, backups, logging, training, retainer, tabletop exercises. Everything else fails without this.
2. **Detection and Analysis** — validate the alert, scope the compromise, determine severity, preserve evidence.
3. **Containment** — short-term (isolate host, block IP, disable account) then long-term (rebuild, segment).
4. **Eradication** — remove persistence, malware, rogue accounts; patch the entry point.
5. **Recovery** — restore from known-good, monitor closely, phase back into production.
6. **Post-Incident Activity** — timeline, root cause, cost, lessons learned, detection and control improvements.

Some models add "Coordination/Communication" as a continuous phase — legal, PR, regulators, customers, insurers.

## Severity and escalation

Define before the incident: what is a P1 (ransomware in production, data exfiltration, domain admin compromise) vs P3 (single infected laptop, contained). Specify who can declare an incident, who can authorise taking production offline, and who talks to the press.

## Containment trade-offs

Isolation stops spread but preserves attacker intelligence? Or do you watch (carefully) to understand scope? Rule: **contain when the damage rate exceeds the intelligence value**. Never let "we want to see what they do" delay protecting backups.

## Evidence handling

Preserve volatile data before shutdown: memory, network connections, process list, logged-in users. Image disks if prosecution or deep forensics is likely. Maintain chain of custody ([[Digital Forensics]]).

## Communication

Single incident commander, one channel, timestamped notes, pre-approved holding statements, legal privilege considerations, and regulatory clocks — GDPR 72 hours, [[DPDP Act 2023]] breach notification, [[PCI DSS]] obligations, sector regulators.

## Common failures

- No out-of-hours contact path; hours lost finding someone.
- Backups unreachable or untested ([[Backup and Recovery]]).
- IR team without authority to isolate a C-level's laptop.
- No logging retention to reconstruct the timeline.
- Skipping lessons learned — the same incident recurs.

## Related

- [[Digital Forensics]]
- [[SIEM]]
- [[SOAR]]
- [[Ransomware]]
- [[Business Continuity and Disaster Recovery]]
- [[Defensive Ops MOC]]
