---
title: SOC 2
aliases: [SOC2, Service Organization Control 2, Type II]
category: grc
tags: [grc/attestation, saas]
status: developing
up: "[[GRC MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: ["AICPA Trust Services Criteria"]
---

# SOC 2

## Summary

An AICPA attestation report on a service organisation's controls, built on the **Trust Services Criteria**. The de facto vendor-assurance document for SaaS: customers will ask for it during procurement, and "SOC 2 Type II" is often a sales prerequisite.

## Trust Services Criteria

- **Security** (required) — the common criteria.
- **Availability**
- **Processing integrity**
- **Confidentiality**
- **Privacy**

Most companies scope Security plus whichever others their customers demand.

## Type I vs Type II

- **Type I** — controls suitably designed at a point in time (snapshot).
- **Type II** — controls operating effectively over a period (usually 6–12 months). This is the one that matters; it requires evidence collection across the whole window.

## Evidence that matters

Access reviews, change management approvals, vulnerability scans and remediation, incident records, backup restore tests, onboarding/offboarding tickets, monitoring alerts and responses, risk assessments, policy acknowledgements.

## Practicalities

- **Readiness assessment** first; tooling (Vanta, Drata, Secureframe) automates evidence collection but cannot invent controls.
- The audit is performed by a CPA firm; the report goes to customers under NDA.
- Common failure: policies written but not followed, and no evidence of operation (e.g. access reviews done once and never again).
- Scope carefully — every system in scope adds evidence burden.

## Relation to other frameworks

Security criteria overlap heavily with [[ISO 27001]] Annex A and [[NIST CSF]]; many organisations maintain both for different markets.

## Related

- [[ISO 27001]]
- [[Compliance Audit]]
- [[GDPR]]
- [[GRC MOC]]
