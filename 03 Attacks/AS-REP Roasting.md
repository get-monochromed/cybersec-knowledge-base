---
title: AS-REP Roasting
aliases: [AS-REP Roasting, ASREPRoast, T1558.004]
category: attack
tags: [attack/host, credential, active-directory]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# AS-REP Roasting

## Summary

Cracking a Kerberos AS-REP for any account that has **"Do not require Kerberos pre-authentication"** set. The KDC returns material encrypted with that user's password key without proving the requester knows anything, so the attack needs only a valid **username** — no password, no session, no domain foothold.

## How it works

1. Find accounts with `DONT_REQ_PREAUTH` (UF_DONT_REQUIRE_PREAUTH, `0x400000`): LDAP filter `(userAccountControl:1.2.840.113556.1.4.803:=4194304)`.
2. Request an AS-REQ for each — the KDC replies with an AS-REP encrypted with the user's key.
3. Crack offline: `GetNPUsers.py domain/ -usersfile users.txt -format hashcat`, then `hashcat -m 18200` (RC4) / `-m 19900` (AES).
4. Log in with the recovered password.

It is a **pre-authentication bypass**: normal accounts must prove knowledge of their key before the KDC responds, which is exactly what blocks offline cracking. Disabling pre-auth removes that protection — usually a legacy compatibility setting from before Windows 2008.

## Detection

- **4768** AS-REQ without pre-authentication (`PreAuthType 0`) — this is the direct signal.
- Bulk 4768 failures/successes for many accounts from one host (user enumeration of vulnerable accounts).
- LDAP queries filtering on `userAccountControl` bit 4194304.
- Any account with pre-auth disabled at all — treat as a misconfiguration finding, not just a logging one.

## Mitigation

- **Require Kerberos pre-authentication** on every account (the default; audit for exceptions).
- Long random passwords (25+) for any account that genuinely cannot change.
- Disable RC4; enforce AES.
- Monitor 4768 with `PreAuthType 0` and alert ([[Sigma Rules]]).
- Include the UAC flag in AD hygiene reports alongside "password never expires" and "unconstrained delegation".

## Related

- [[Kerberos]]
- [[Kerberoasting]]
- [[Password Attacks]]
- [[Operating System Security]]
- [[Attacks MOC]]
