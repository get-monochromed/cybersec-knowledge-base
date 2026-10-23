---
title: Kerberos Delegation
aliases: [Kerberos Delegation Abuse, Unconstrained Delegation, RBCD, S4U]
category: attack
tags: [attack/host, active-directory, privilege]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Kerberos Delegation

## Summary

Delegation lets a service act on a user's behalf to reach another service — legitimate middleware behaviour, and one of the most reliable paths to domain admin when misconfigured. Three flavours, each with a different abuse.

## The three types

| Type | How it works | Risk |
|---|---|---|
| **Unconstrained** | The service receives the user's full TGT and can impersonate them to *any* service | Steal TGTs from LSASS; if the host is a DC or a server admins log into, game over |
| **Constrained (KCD)** | The service may only impersonate to a fixed list of SPNs (`msDS-AllowedToDelegateTo`) | Abuse via S4U2Self + S4U2Proxy if it can proxy to a privileged service |
| **Resource-based constrained (RBCD)** | The *target* decides who may impersonate to it (`msDS-AllowedToActOnBehalfOfOtherIdentity`) | Anyone who can write that attribute on a computer object gains access as any user — often a short hop from generic write |

## How the abuse looks

- **Unconstrained** — `TRUSTED_FOR_DELEGATION` accounts/hosts: coerce authentication (PrinterBug/PetitPotam), capture the machine or user TGT, then use it ([[Pass-the-Hash|pass-the-ticket]]). Domain controllers are trusted for delegation by default.
- **Constrained** — request a service ticket for the service, use S4U2Self to get a ticket "as" an admin, then S4U2Proxy to the allowed SPN.
- **RBCD** — write `msDS-AllowedToActOnBehalfOfOtherIdentity` on the target (typically a computer where you have write rights), create a machine account, then S4U2Proxy to it. Popular because it needs no privileged service account hash.

## Detection

- **4741/4742** computer object changes mentioning `msDS-AllowedToActOnBehalfOfOtherIdentity`.
- Accounts/hosts with `TRUSTED_FOR_DELEGATION` — audit them; they should be rare and privileged.
- **4769** with `S4U2Self`/`S4U2Proxy` (transited services) to unexpected SPNs.
- Coercion artefacts: spooler service abuse (MS-RPRN), EFSRPC calls, unusual machine authentication bursts.
- Anomalous `Domain Computers` membership additions (machine account quota abuse).

## Mitigation

- **Remove unconstrained delegation** everywhere except DCs; mark sensitive accounts "Account is sensitive and cannot be delegated" and add them to **Protected Users**.
- Move to **RBCD or constrained delegation** with the narrowest SPN list.
- Tighten ACLs on computer objects — `GenericWrite`/`GenericAll` on a computer is effectively delegation abuse.
- Disable the **Print Spooler** service on DCs and servers that do not print (blocks the classic coercion).
- Reduce `MachineAccountQuota` from the default 10 to 0.
- Audit delegation flags and RBCD attributes continuously; alert on changes ([[Sigma Rules]]).

## Related

- [[Kerberos]]
- [[Golden Ticket]]
- [[Privilege Escalation]]
- [[Lateral Movement]]
- [[Active Directory Certificate Services (ADCS)]]
- [[Attacks MOC]]
