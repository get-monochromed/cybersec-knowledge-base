---
title: Kerberos
aliases: [Kerberos Protocol, KRB5, TGT, TGS]
category: foundation
tags: [foundation/core, identity, windows, exam]
status: solid
up: "[[Foundations MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Kerberos

## Summary

The default authentication protocol in Active Directory (and in MIT/Heimdal realms). A trusted third party — the **KDC**, which runs on every domain controller — issues time-limited **tickets** that prove identity. Understanding the ticket flow is the prerequisite for every AD attack: Kerberoasting, AS-REP roasting, golden and silver tickets, and delegation abuse all fall out of it.

## The three parties

- **Client** — a user or computer with a secret derived from its password (NTLM hash / AES key).
- **KDC** — Authentication Service (AS) + Ticket Granting Service (TGS), running on the DC.
- **Service** — the target application (file share, SQL, HTTP), identified by an **SPN** (Service Principal Name).

## Ticket flow

1. **AS-REQ / AS-REP** — client pre-authenticates with a timestamp encrypted using its key; the KDC returns a **TGT** (Ticket Granting Ticket) encrypted with the **krbtgt** account hash, plus a session key encrypted with the client's key.
2. **TGS-REQ / TGS-REP** — for each service, the client presents the TGT and requests a **service ticket** for that SPN. The service ticket is encrypted with the **service account's** key.
3. **AP-REQ** — the client presents the service ticket to the service, which decrypts it with its own key and trusts the identity inside (including the **PAC**, which carries group membership).

Ports: 88 TCP/UDP. Time skew must be under ~5 minutes or authentication fails — which is why NTP matters for both availability and logs.

## Why it matters for attacks

| Property | Consequence |
|---|---|
| Service tickets are encrypted with the service account's key | Anyone who can request a ticket can take it offline and crack it → [[Kerberoasting]] |
| Pre-auth can be disabled per account | AS-REP returned encrypted with the user's key, crackable without credentials → [[AS-REP Roasting]] |
| krbtgt signs all TGTs | Its hash forges unlimited access → [[Golden Ticket]] |
| Service keys sign their own tickets | Forged service ticket with no DC contact → [[Silver Ticket]] |
| Delegation lets a service impersonate users | Abuse to reach other services → [[Kerberos Delegation]] |

Encryption types matter: **RC4-HMAC (0x17)** tickets are far cheaper to crack than **AES256 (0x12)**, so disabling RC4 (and enforcing AES) both strengthens the domain and makes roasting noisier.

## Weaknesses and hardening

- **No channel binding by default** → relay attacks (NTLM relay, ADCS ESC8).
- **NTLM fallback** keeps hash-reuse attacks alive ([[Pass-the-Hash]]); restrict or audit NTLM.
- **Long ticket lifetimes** (default 10 h, renewable 7 days) widen the window for stolen tickets.
- **krbtgt never rotated** → one compromise is permanent.
- Protect **Tier 0**: Domain Admins, DCs, krbtgt, ADCS. Enforce `Protected Users`, disable unconstrained delegation, audit SPNs and ACLs.

## Related

- [[Authentication, Authorization and Accounting]]
- [[Security Models]]
- [[Kerberoasting]]
- [[AS-REP Roasting]]
- [[Golden Ticket]]
- [[Silver Ticket]]
- [[Kerberos Delegation]]
- [[Operating System Security]]
- [[Foundations MOC]]
