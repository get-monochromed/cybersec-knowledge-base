---
title: Business Email Compromise
aliases: [BEC, CEO Fraud, Invoice Fraud, EAC]
category: attack
tags: [attack/social, fraud]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Business Email Compromise

## Summary

Impersonating or hijacking a business email account to redirect money or data. No malware required, losses dwarf most ransomware payments, and the whole attack is often a few emails. FBI IC3 consistently ranks BEC among the highest-loss cybercrime categories.

## How it works

1. **Access** — compromised mailbox ([[Phishing]], credential stuffing, [[Password Attacks]]) or a convincing lookalike domain.
2. **Study** — read threads, learn suppliers, payment cycles, who approves what, when the CFO is travelling (out-of-office replies are reconnaissance).
3. **Pretext** — changed bank details, urgent wire, gift-card request, W-2/tax data request, "quiet" acquisition.
4. **Leverage** — urgency, authority, secrecy ("don't discuss with the team"), or a hijacked real thread (thread injection) with prior context.
5. **Cash out** — money mules, crypto, or data resale.

## Variants

- **CEO/CFO fraud** — authority + urgency to a junior employee.
- **Vendor email compromise** — supplier's real mailbox hijacked, invoice PDF swapped.
- **Attorney impersonation** — confidential matter, urgent transfer.
- **Payroll diversion** — change direct-deposit details.
- **Thread hijacking** — reply inside a genuine, existing conversation.
- **MFA-fatigue assisted account takeover** — combined with [[Phishing]] variants.

## Detection

- Mailbox rules forwarding or auto-deleting (attacker persistence and concealment).
- Login anomalies: new country/device, legacy protocol use (IMAP/POP), token grants.
- Finance process signals: bank-detail change requests, pressure language, sender domain age/near-miss spelling.
- Out-of-band verification is the control, not a detector.

## Mitigation

- **Callback verification** on any bank-detail change, using a known number — not the one in the email. This single process defeats most BEC.
- **MFA everywhere**, phishing-resistant for finance and executives.
- **DMARC reject** + lookalike-domain monitoring ([[Email Security]]).
- **Mailbox rule alerts**: alert whenever a rule forwards externally or deletes mail.
- **Payment approval separation of duties** ([[Security Principles]]) and dual authorisation.
- **Executive protection**: hardened accounts, device compliance, travel awareness, training for assistants/finance.
- **Recovery playbook**: contact bank fast (recall window is hours), preserve logs, notify law enforcement.

## Related

- [[Phishing]]
- [[Email Security]]
- [[Social Engineering]]
- [[Cybercriminal]]
- [[Attacks MOC]]
