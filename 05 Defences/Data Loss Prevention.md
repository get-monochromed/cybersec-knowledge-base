---
title: Data Loss Prevention
aliases: [DLP, Data Leakage Prevention]
category: defence
tags: [defence/data, privacy]
status: developing
up: "[[Defences MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Data Loss Prevention

## Summary

Controls that detect and block sensitive data leaving its authorised boundary — email, web upload, USB, cloud sync, printing. Technically hard, organisationally harder: it needs a data classification scheme before it can work.

## Prerequisites

1. **Classification** — public / internal / confidential / restricted, with owners.
2. **Inventory** — where the data lives and who touches it.
3. **Policy** — what is allowed, by data type and channel.

Without these, DLP is regex guesswork.

## Channels

- **Endpoint DLP** — USB, clipboard, print, screen capture, app-to-app copy.
- **Network DLP** — HTTP/S uploads, SMTP, FTP; TLS visibility is the usual blocker.
- **Cloud DLP / CASB** — SaaS sharing, personal OneDrive/Dropbox, OAuth apps.
- **Email DLP** — outbound scanning with approval workflow for sensitive content.

## Detection methods

- Pattern matching (PAN, Aadhaar, national ID, IBAN, private keys).
- Document fingerprinting (exact match of known sensitive files).
- ML classification for unstructured data (contracts, source code).
- User behaviour context: bulk download, first-time external recipient, off-hours.

## Operational reality

- **Enforce on high-confidence rules only**; noisy blocks train users to route around the control.
- Start with alerting + education for 30–90 days, then block.
- Integrate with [[Insider Threat]] monitoring and HR/legal process — monitoring must be lawful and disclosed.
- Watch for DLP bypass via personal email, screenshots, and mobile cameras.
- Measure prevented/alerted incidents, not "policies created".

## Related

- [[Insider Threat]]
- [[Cloud Security]]
- [[GDPR]]
- [[DPDP Act 2023]]
- [[Defences MOC]]
