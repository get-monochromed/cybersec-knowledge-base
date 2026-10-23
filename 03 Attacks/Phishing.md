---
title: Phishing
aliases: [Phishing Attack, Spear Phishing, Smishing, Vishing]
category: attack
tags: [attack/social, initial-access, exam]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Phishing

## Summary

Deceiving a person into an action — clicking a link, opening an attachment, entering credentials, approving an MFA prompt, paying an invoice. Still the most common initial access route, because it attacks the human layer where no patch exists.

## How it works

1. **Recon** — harvest names, roles, relationships, email format, suppliers ([[Reconnaissance]]).
2. **Pretext** — a believable reason: invoice, password expiry, HR policy, shared document, delivery notice.
3. **Delivery** — email, SMS (smishing), voice (vishing), Teams/Slack message, calendar invite, QR code (quishing).
4. **Action** — credential entry on a cloned page, malware attachment, OAuth consent, MFA approval, payment change.
5. **Exploitation** — credential use, session token theft, [[Business Email Compromise]], [[Ransomware]] payload.

## Variants

- **Bulk/commodity phishing** — generic, high volume, low effort.
- **Spear phishing** — researched, targeted, personalised; the [[Advanced Persistent Threat|APT]] entry point.
- **Whaling** — targets executives (CEO fraud, authorised payment requests).
- **Clone phishing** — copy of a real prior email with swapped links/attachments.
- **Vishing** — phone; often pairs with helpdesk impersonation for MFA reset (see [[Social Engineering]]).
- **Smishing / quishing** — SMS and QR codes to bypass email filtering and desktop protections.
- **Adversary-in-the-middle (AiTM)** — proxy (Evilginx-style) that steals the session cookie *after* MFA. Defeats plain MFA; needs phishing-resistant FIDO2.
- **OAuth consent phishing** — grant a malicious app access; no password needed.
- **MFA fatigue / push bombing** — spam push prompts until the user approves, or call and claim to be IT.

## Detection

- Mail gateway signals: new domain age, SPF/DKIM/DMARC failures, lookalike domains (homoglyphs), reply-to mismatch, first-time sender, unusual attachment types (`.html`, `.iso`, `.lnk`, macro-enabled docs).
- Endpoint: Office spawning PowerShell/`mshta`/`rundll32` ([[Living off the Land]]).
- Identity: impossible travel, new device, mass MFA prompts, OAuth grants (`Mail.Read`, `offline_access`), inbox rules created.
- User reports — the best sensor; make reporting one click ([[Security Awareness Training]]).

## Mitigation

- **Technical, not just training**: DMARC enforcement ([[Email Security]]), link isolation/detonation, attachment sandboxing, external-sender banners.
- **Phishing-resistant MFA** (FIDO2/[[Passkeys]]) — the only real fix for AiTM.
- **Conditional access** and token binding: device compliance, impossible-travel blocks.
- **Least privilege**: a phished user should not be able to approve payments or reach production ([[Access Control Models]]).
- **Simulation + training** — useful if realistic and not punitive; measure report rate, not click rate alone.
- **Playbook**: credential reset, session revocation, mailbox rule audit, check for a second victim.

## Related

- [[Business Email Compromise]]
- [[Social Engineering]]
- [[Email Security]]
- [[Security Awareness Training]]
- [[Password Attacks]]
- [[Attacks MOC]]
