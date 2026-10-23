---
title: Golden Ticket
aliases: [Golden Ticket Attack, Forged TGT, T1558.001]
category: attack
tags: [attack/host, credential, active-directory, persistence]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Golden Ticket

## Summary

A forged **TGT** signed with the **krbtgt** account's hash. Because every TGT in the domain is signed by krbtgt, an attacker holding that hash can mint a ticket for any user — including a non-existent one — with any group membership, valid for as long as they choose (commonly 10 years).

## How it works

1. Obtain the krbtgt hash — DCSync ([[DCSync]]), NTDS.dit copy, or a DC compromise.
2. Note the domain SID and krbtgt RID (502).
3. Forge: `kerberos::golden /user:fake /domain:corp.local /sid:S-1-5-21-... /krbtgt:<hash> /ptt`.
4. The attacker now has domain-wide access — including to systems they have never authenticated to — until krbtgt is rotated **twice** (the current and previous keys both sign valid tickets).

## Why it is so damaging

- **No DC interaction to use it** — the forged TGT is presented directly to services; nothing appears in DC logs.
- **Persistence that survives password resets** — resetting the compromised user's password does not invalidate a forged ticket.
- **Any identity, any privileges** — including Domain Admin, Enterprise Admin, or a fictitious account.

## Detection

- **TGT use without a preceding 4768** (AS-REQ) on the DC — the primary signal. Requires centralised DC logging.
- Anomalous ticket properties: lifetime far beyond policy, unknown SIDs, unexpected encryption types, PAC validation failures.
- **4769** issued for services by an account that never authenticated.
- Kerberos errors on services (`KDC_ERR_TGT_REVOKED`, PAC signature failures) after krbtgt rotation — a sign that forged tickets stopped working.
- Impossible: "no logon event but resource access occurred" — correlate DC and member-server logs ([[SIEM]]).

## Mitigation and response

- **Rotate krbtgt twice**, with a wait longer than the maximum ticket lifetime between rotations (typically 10 h; often done as two rotations 10–24 h apart). This invalidates forged tickets.
- Protect **Tier 0**: DCs, krbtgt, ADCS, backup infrastructure. No Tier 0 credential ever logs into a workstation.
- **DCSync rights audit** and alerting ([[DCSync]]).
- 25+ character krbtgt password; monitor its last-set date.
- After a suspected golden ticket: treat the domain as compromised, rotate krbtgt, reset privileged credentials twice, hunt for persistence ([[Incident Response]]).

## Related

- [[Kerberos]]
- [[Silver Ticket]]
- [[DCSync]]
- [[Kerberos Delegation]]
- [[Privilege Escalation]]
- [[Attacks MOC]]
