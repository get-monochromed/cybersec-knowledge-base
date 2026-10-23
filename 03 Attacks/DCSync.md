---
title: DCSync
aliases: [DCSync, Directory Replication Service Abuse, T1003.006]
category: attack
tags: [attack/host, credential, active-directory]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# DCSync

## Summary

Impersonating a domain controller and asking a real DC to replicate account secrets over the DRSUAPI protocol. Instead of touching `NTDS.dit` on a DC, the attacker pulls password hashes — including krbtgt — remotely, with legitimate protocol traffic.

## How it works

1. The attacker's account needs replication rights: **Domain Admin**, **Enterprise Admin**, or an explicit ACE granting *Replicating Directory Changes* / *Replicating Directory Changes All* (plus *Replicating Directory Changes in Filtered Set* for some paths). Misconfigured ACLs and leftover service accounts are the usual source.
2. `mimikatz lsadump::dcsync /domain:corp.local /user:krbtgt`, or Impacket's `secretsdump.py -just-dc-user krbtgt`.
3. The DC returns the account's secrets, which feed [[Golden Ticket]] / [[Pass-the-Hash]].

It requires no code execution on a DC and no malware — one of the quietest ways to reach Tier 0.

## Detection

- **4662** (directory service access) on the DC with the replication GUIDs:
  - `1131f6aa-9c07-11d1-f79f-00c04fc2dcd2` — Replicating Directory Changes
  - `1131f6ad-9c07-11d1-f79f-00c04fc2dcd2` — Replicating Directory Changes All
  - `89e535c8-fca6-4174-b1b8-200e2b1f3b3c` — Replicating Directory Changes in Filtered Set
- 4662 by a non-DC account, especially for `krbtgt`, `Administrator`, or in bulk.
- DRSUAPI traffic from a workstation or member server.
- Anomalous accounts with replication ACEs — audit AD ACLs (BloodHound, `dsacls`) rather than waiting for the alert.

## Mitigation

- **Audit and remove** unnecessary replication permissions; treat any account with them as Tier 0.
- Alert on the three GUIDs above ([[Sigma Rules]]); baseline which accounts legitimately replicate (only DCs, and Azure AD Connect sync accounts).
- **Tier 0 isolation**: DCs and accounts with replication rights never log into tier-1/tier-2 systems.
- Honeytoken: a decoy account that should never be touched; any replication of it is an alarm.
- After a suspected DCSync: assume every hash is compromised — rotate krbtgt twice, reset privileged accounts, rebuild privileged workstations ([[Incident Response]]).

## Related

- [[Golden Ticket]]
- [[Silver Ticket]]
- [[Kerberos]]
- [[Privilege Escalation]]
- [[Operating System Security]]
- [[Attacks MOC]]
