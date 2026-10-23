---
title: HIPAA
aliases: [HIPAA, Health Insurance Portability and Accountability Act, PHI]
category: grc
tags: [grc/law, healthcare, us]
status: developing
up: "[[GRC MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# HIPAA

## Summary

US law protecting **Protected Health Information (PHI)**. Two rules matter for security: the **Security Rule** (technical, physical and administrative safeguards) and the **Breach Notification Rule**. Applies to covered entities (providers, insurers, clearinghouses) and their business associates.

## Key concepts

- **PHI** — health information linked to an individual, in any form.
- **Covered entity** vs **Business Associate** (vendor handling PHI; needs a BAA — Business Associate Agreement).
- **Minimum necessary** principle for access and disclosure.
- **Security Rule**: administrative (risk analysis, policies, training), physical (facility access, devices), technical (access control, audit logging, integrity, transmission security, authentication).
- **Breach notification**: individuals within 60 days; HHS; media if >500 people in a state.
- **Encryption safe harbour** — properly encrypted PHI is not "unsecured" if lost, which is why encryption at rest is universal in healthcare.

## Practical controls

Access control and audit logging on EHR systems, unique user IDs (no shared logins), automatic logoff, encryption in transit and at rest, contingency/backup plans, device and media controls, BAAs with every vendor touching PHI, and annual security risk analysis.

## Honest note

HIPAA is deliberately technology-neutral and vague ("reasonable safeguards"), so enforcement varies; auditors and customers fill the gap with frameworks like [[NIST CSF]] and HITRUST. Non-compliance penalties scale with negligence, up to criminal liability for knowing misuse.

## Related

- [[GDPR]]
- [[DPDP Act 2023]]
- [[Compliance Audit]]
- [[GRC MOC]]
