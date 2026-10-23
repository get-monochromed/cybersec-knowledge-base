---
title: Backup and Recovery
aliases: [Backups, 3-2-1 Rule, Restore, RTO, RPO]
category: defence
tags: [defence/recovery, ransomware, exam]
status: solid
up: "[[Defences MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Backup and Recovery

## Summary

The control that converts a destructive attack into an inconvenience. Untested backups are a belief, not a control — the only meaningful metric is *time to restore service from a clean copy*.

## The 3-2-1-1-0 rule

- **3** copies of data
- **2** different media/locations
- **1** offsite
- **1** offline or immutable (tape, air-gapped, object lock)
- **0** errors on verified restore tests

## Key terms

- **RPO** (recovery point objective) — how much data you can afford to lose (drives backup frequency).
- **RTO** (recovery time objective) — how fast you must be back (drives architecture, not backup software).
- **Retention** — daily/weekly/monthly/yearly; also a legal requirement ([[GDPR]], [[PCI DSS]]).
- **Immutable/object lock** — storage that cannot be deleted or encrypted even by a compromised admin (or at least not until retention expires).

## Ransomware-specific design

- **Separate the control plane**: backup admin credentials must not be domain admin — attackers target the backup console first.
- **Pull-based replication** — the backup server fetches from production; production credentials cannot reach the backup store.
- **MFA + offline copies of the catalogue**; protect against deletion of the catalog itself.
- **Test restore to an isolated environment** quarterly; measure actual RTO, not the vendor's claim.
- **Verify integrity** (checksums) and scan restore images before returning to service.

## Other failure modes

- Snapshots are not backups (same storage, same credentials, encrypted together).
- Replication is not a backup (deletes and encryption replicate).
- Backups in the same domain/tenant as production.
- No restore documentation — the one person who knew left.
- Backup jobs silently failing for months; alert on job success as a monitored control.

## Cloud

Versioning + object lock + cross-account/cross-region copies; separate KMS keys; protect the root account ([[Cloud Security]]).

## Related

- [[Ransomware]]
- [[Business Continuity and Disaster Recovery]]
- [[Incident Response]]
- [[Network Segmentation]]
- [[Defences MOC]]
