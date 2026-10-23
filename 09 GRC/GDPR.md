---
title: GDPR
aliases: [General Data Protection Regulation, EU GDPR]
category: grc
tags: [grc/privacy, law, eu]
status: solid
up: "[[GRC MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: ["Regulation (EU) 2016/679"]
---

# GDPR

## Summary

The EU's data protection regulation, in force since 2018. It applies to any organisation processing EU residents' personal data, regardless of where the organisation is located — which is why it became the global template for privacy law ([[DPDP Act 2023]] follows a similar shape).

## Principles (Article 5)

1. Lawfulness, fairness, transparency
2. Purpose limitation
3. Data minimisation
4. Accuracy
5. Storage limitation
6. Integrity and confidentiality (security)
7. **Accountability** — you must be able to *prove* compliance

## Lawful bases (Article 6)

Consent, contract, legal obligation, vital interests, public task, legitimate interests. Security teams mostly work under legal obligation or legitimate interests; consent is the weakest base for security processing.

## Roles

- **Controller** — decides why and how data is processed.
- **Processor** — processes on the controller's behalf (cloud providers, SaaS).
- **DPO** — data protection officer, required in some cases.
- **Supervisory authority** — the regulator (e.g. ICO, CNIL, DPC).

## Security-relevant obligations

- **Article 32** — appropriate technical and organisational measures: encryption, pseudonymisation, confidentiality/integrity/availability, resilience, testing. This is where [[ISO 27001]] and [[NIST CSF]] map in.
- **Article 33** — breach notification to the regulator within **72 hours** of becoming aware, unless unlikely to result in risk.
- **Article 34** — notify affected individuals when risk is high.
- **Article 30** — records of processing activities (ROPA).
- **Article 35** — DPIA for high-risk processing.
- **Articles 15–22** — data subject rights: access, rectification, erasure, restriction, portability, objection, automated decision-making.
- **Article 28** — written processor contracts, due diligence on vendors ([[Supply Chain Attack]]).

## Penalties

Two tiers: up to **€10m or 2%** of global annual turnover (administrative failures), up to **€20m or 4%** (principle violations, unlawful processing), whichever is higher.

## Practical implications for security

- Log retention and monitoring must be proportionate and documented (your [[SIEM]] sees personal data).
- Pseudonymise in analytics; restrict access to raw personal data ([[Access Control Models]]).
- Breach playbooks must include the 72-hour clock and the decision-maker ([[Incident Response]]).
- Third-party risk is a legal obligation, not just good practice.
- "Security incident" ≠ "personal data breach" — the latter triggers notification.

## Related

- [[DPDP Act 2023]]
- [[Data Loss Prevention]]
- [[Incident Response]]
- [[ISO 27001]]
- [[GRC MOC]]
