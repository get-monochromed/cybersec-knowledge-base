---
title: Compliance Audit
aliases: [Audit, Internal Audit, Certification, Assurance]
category: grc
tags: [grc/assurance, audit]
status: solid
up: "[[GRC MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Compliance Audit

## Summary

Independent examination of whether controls exist and operate as claimed. The output is a finding set and an opinion — certification, attestation, or a management letter — that customers, regulators and insurers rely on.

## Types

- **Internal audit** — first line of assurance, reports to management/board.
- **External audit / certification** — ISO 27001, PCI QSA, SOC 2 CPA.
- **Regulatory examination** — sector regulators (RBI, SEBI, ICO, etc.).
- **Customer audits / questionnaires** — SIG, CAIQ, bespoke.
- **Attestation vs certification** — SOC 2 is an attestation on controls; ISO 27001 is certification of a management system.

## Evidence types

Policies and approvals · access review records · change tickets and approvals · vulnerability scan results and remediation · backup restore test logs · incident records · training completion · supplier assessments · meeting minutes · screenshots of configuration.

**Point-in-time evidence is a red flag.** Auditors increasingly sample across the period, so evidence must exist continuously — which is why automating evidence collection matters (see [[SOC 2]]).

## How audits fail

- Policies written but not implemented (the classic).
- Scope declared smaller than reality (shadow IT, unmanaged cloud accounts).
- No evidence of *operation* — a procedure document is not proof it ran.
- Findings with no owner, no due date, or silently accepted.
- Last-minute scramble; the audit becomes a documentation exercise in fiction.

## Getting value from it

- Treat findings as free risk assessment; prioritise by real impact, not by audit severity labels.
- Use a **control matrix** mapping framework control → your control → owner → evidence source → test method.
- Track audit findings in the same risk register as everything else ([[Risk Management]]).
- Remember: compliant ≠ secure. The gap is where incidents happen.

## Related

- [[ISO 27001]]
- [[PCI DSS]]
- [[SOC 2]]
- [[Security Policy]]
- [[GRC MOC]]
