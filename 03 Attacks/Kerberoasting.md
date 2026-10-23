---
title: Kerberoasting
aliases: [Kerberoast, SPN Roasting, T1558.003]
category: attack
tags: [attack/host, credential, windows, active-directory]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Kerberoasting

## Summary

Requesting a Kerberos service ticket for an account that has an **SPN**, then cracking that ticket offline. The ticket is encrypted with the service account's password-derived key, so the crack happens on the attacker's hardware with no noise on the target and no special privileges — any authenticated domain user can do it.

## How it works

1. Enumerate accounts with SPNs: `GetUserSPNs.py domain/user:pass -request`, `Rubeus kerberoast`, or LDAP filter `(servicePrincipalName=*)`.
2. Request a TGS for each SPN. The DC returns it encrypted with the service account's key (RC4 or AES).
3. Crack offline with `hashcat -m 13100` (RC4/TGS-REP) or `-m 19700` (AES).
4. Use the recovered password for [[Lateral Movement]] or further privilege escalation.

Service accounts are the target because they are often old, over-privileged, and have human-chosen passwords that never expire.

## Why RC4 matters

RC4-HMAC tickets crack dramatically faster than AES tickets (hashcat mode 13100 vs 19700). If the domain still permits RC4, the attacker requests RC4 tickets even where AES is supported. Disabling RC4 is therefore both a hardening measure and a noise generator.

## Detection

- **4769** (TGS request) with **encryption type 0x17** (RC4) where AES is expected — the classic high-fidelity signal.
- Volume: one user requesting many distinct SPNs in a short window.
- Requests from hosts that never normally request those services; service accounts with SPNs that are never actually used.
- Honeypot SPN: a decoy account with an SPN that no legitimate client ever requests.

## Mitigation

- **Managed service accounts (gMSA)** with 240-character machine-managed passwords — uncrackable in practice.
- 25+ character random passwords for accounts that cannot use gMSA; rotate on a schedule.
- **Disable RC4**, enforce AES for Kerberos.
- Remove unnecessary SPNs; audit which service accounts hold them.
- Least privilege for service accounts — a cracked service account should not be a domain admin.
- Monitor 4769 volume and RC4 downgrades; alert on both ([[Sigma Rules]], [[SIEM]]).

## Related

- [[Kerberos]]
- [[AS-REP Roasting]]
- [[Password Attacks]]
- [[Operating System Security]]
- [[Attacks MOC]]
