---
title: Email Security
aliases: [Email Security Domain, SPF, DKIM, DMARC]
category: domain
tags: [domain/email, phishing]
status: solid
up: "[[Domains MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Email Security

## Summary

Email is still the primary delivery mechanism for [[Phishing]] and [[Business Email Compromise]]. Defence is layers: authentication of senders, filtering of content, and isolation of links/attachments.

## Sender authentication

- **SPF** — DNS TXT record listing IPs allowed to send for the domain. Breaks on forwarding; not aligned to the visible From header.
- **DKIM** — cryptographic signature of the message, verified via a DNS public key. Proves integrity and domain association.
- **DMARC** — policy (`none`/`quarantine`/`reject`) + alignment + reporting (rua/ruf). This is the control: publish `p=reject` with `sp=reject` and monitor reports.
- **BIMI/MTA-STS/DANE** — branding and transport security; nice-to-have.

Without DMARC enforcement, anyone can spoof your domain. With it, attackers move to lookalike domains — monitor registrations ([[DNS Attacks]]).

## Filtering and isolation

- Inbound: reputation, attachment sandboxing/detonation, macro and `.html`/`.iso`/`.lnk` blocking, impersonation protection (display-name and lookalike detection), external-sender banners.
- Links: URL rewriting + time-of-click analysis, or full remote browser isolation.
- Outbound: DLP, compromised-mailbox detection (bulk sends, new rules).
- **DMARC/ARC** handling for legitimate third-party senders.

## Detection and response

- Alerts on: new inbox rules forwarding externally, mass mail from one account, first-time sender with urgency, OAuth grants, impossible travel.
- Report button → triage queue → hunt for other recipients ([[Incident Response]]).
- Preserve headers (full `.eml`) for investigation — they contain the true path and auth results.

## Related

- [[Phishing]]
- [[Business Email Compromise]]
- [[DNS Attacks]]
- [[Data Loss Prevention]]
- [[Domains MOC]]
