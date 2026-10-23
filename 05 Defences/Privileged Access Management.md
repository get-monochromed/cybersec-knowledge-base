---
title: Privileged Access Management
aliases: [PAM, Just-in-Time Access, JIT, Credential Vaulting]
category: defence
tags: [defence/identity, access-control, privileged]
status: solid
up: "[[Defences MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Privileged Access Management

## Summary

Controlling the accounts that can destroy the organisation: admin accounts, service accounts, root, domain admin, cloud root, backup and hypervisor consoles. PAM is the discipline of removing standing privilege — vault it, broker it, time-box it, record it, and prove you did.

## Why it matters

Almost every serious breach escalates through privilege. Tier 0 credentials on a workstation, shared local admin passwords, and permanent domain admin accounts are what turn a phished laptop into a ransomware event ([[Pass-the-Hash]], [[Lateral Movement]], [[Golden Ticket]]).

## Components

- **Credential vaulting** — secrets stored in a PAM system, checked out per session with approval, rotated automatically after use.
- **Just-in-time (JIT) elevation** — privilege granted for minutes, tied to a ticket/approval, then removed. Replaces permanent admin group membership.
- **Session brokering and recording** — access goes through a jump host/proxy; keystrokes, commands and file transfers are logged (deterrent + evidence).
- **Privileged session management (PSM)** — RDP/SSH/DB proxying without exposing credentials to the user's endpoint.
- **Secrets management for machines** — service accounts, API keys, certificates ([[Key Management]]).
- **Break-glass accounts** — sealed, monitored, offline credentials for when PAM itself is down.

## Operating model

1. **Inventory** all privileged accounts, service accounts, and where their credentials live.
2. **Reduce** — eliminate shared accounts, remove standing admin, convert services to gMSA/managed identities.
3. **Isolate** — tiered admin model: separate accounts per tier (Tier 0 AD/CA, Tier 1 servers, Tier 2 workstations), privileged access workstations (PAW).
4. **Broker** — all admin access via PAM with approval and recording.
5. **Monitor** — every checkout, every elevation, every break-glass use is an alert, not a log line.
6. **Recertify** quarterly; prune accounts nobody uses.

## Metrics worth reporting

- Number of permanent domain admins (target: near zero).
- % of privileged sessions brokered and recorded.
- Mean elevation duration; number of JIT requests vs standing rights.
- Break-glass usage (should be rare and always investigated).
- Age of service account passwords still not managed.

## Failure modes

- PAM deployed as a password vault only, leaving permanent admin rights in place.
- Vault admin credentials accessible from the same workstation the attacker controls.
- Break-glass account with no monitoring and a password from 2019.
- Session recording nobody reviews — deterrent value only if known.

## Related

- [[Access Control Models]]
- [[Authentication, Authorization and Accounting]]
- [[Zero Trust Architecture]]
- [[Operating System Security]]
- [[Defences MOC]]
