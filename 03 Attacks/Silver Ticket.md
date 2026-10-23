---
title: Silver Ticket
aliases: [Silver Ticket Attack, Forged TGS, T1558.002]
category: attack
tags: [attack/host, credential, active-directory, evasion]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Silver Ticket

## Summary

A forged **service ticket (TGS)** signed with a specific service account's key. It grants access to that one service without any contact with the domain controller, so the DC logs show nothing at all — the appeal is stealth and precision, not breadth.

## How it works

1. Obtain the service account's hash (or a computer account's machine hash, `$` accounts).
2. Forge with `kerberos::golden /service:cifs /target:server.corp.local /rc4:<hash> /sid:... /ptt` (mimikatz uses the same `golden` module; the `service` parameter makes it a silver ticket).
3. Access the service: SMB share, MSSQL, HTTP, WMI, scheduled tasks.

Common targets are service accounts with SPNs that also hold local admin rights on servers — CIFS/HOST SPNs are especially useful.

## Golden vs silver

| | Golden ticket | Silver ticket |
|---|---|---|
| Signed with | krbtgt hash | one service/computer account hash |
| Scope | entire domain | one service on one (or several) host(s) |
| DC contact | none to use | none at all |
| DC logs | DC sees the ticket being used in some flows | **nothing** |
| Detection | TGT use without 4768 | target-host logs only |
| Effort | requires DC-level compromise | requires one service account hash |

## Detection

- **On the target host, not the DC**: 4624 logon type 3 with Kerberos but **no corresponding 4769 on any DC** for that account — the core signature.
- Service-side event logs showing access by an account that never authenticated.
- PAC validation failures where the service validates the PAC against the DC (rarely enabled, but decisive when it is).
- Anomalous ticket lifetimes and encryption types; SMB session to a share never used before.

## Mitigation

- **Strong, rotated service account passwords** (gMSA) — the attack requires the service key.
- Machine account password rotation (default 30 days) limits the window for computer-account hashes.
- **Enable PAC validation** where feasible; enable Kerberos armouring (FAST) for sensitive services.
- Service accounts must not be local admins; services should run as `gMSA` with minimal rights.
- Centralise target-host logons into the [[SIEM]] and correlate against DC 4769 events.
- Rotate service account secrets after any suspected compromise; a forged ticket keeps working until the key changes.

## Related

- [[Kerberos]]
- [[Golden Ticket]]
- [[DCSync]]
- [[Lateral Movement]]
- [[Attacks MOC]]
