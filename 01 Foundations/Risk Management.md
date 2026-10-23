---
title: Risk Management
aliases: [Risk, Risk Assessment, Risk Treatment, Risk Register]
category: foundation
tags: [foundation/core, risk, grc, exam]
status: solid
up: "[[Foundations MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Risk Management

## Summary

Deciding what to do about uncertainty. Identify risks, score them, treat them, record who accepted what. It is the language that turns technical findings into business decisions — and the reason "critical vulnerability" and "critical risk" are different statements.

## Core vocabulary

- **Risk** = likelihood of a threat exploiting a vulnerability × impact on the asset.
- **Inherent risk** — before controls.
- **Residual risk** — after controls. This is what the business actually carries.
- **Risk appetite** — how much risk the organisation wants to take.
- **Risk tolerance** — how much variation it will accept before acting.
- **Risk register** — the ledger: ID, description, asset, likelihood, impact, score, owner, treatment, residual, review date.

## Scoring

**Qualitative** — High/Medium/Low matrices. Fast, subjective, fine for most decisions. A 5×5 likelihood/impact heat map is the standard artifact.

**Quantitative** — money:

- **SLE** (single loss expectancy) = asset value × exposure factor
- **ARO** (annualised rate of occurrence)
- **ALE** = SLE × ARO
- **FAIR** — the well-known quantitative methodology (loss event frequency × loss magnitude, Monte Carlo).

Use quantitative when comparing controls with different costs; use qualitative when you need an answer this afternoon.

## Treatment options (the "4 Ts")

| Option | Meaning | Example |
|---|---|---|
| **Mitigate** | Reduce likelihood or impact with a control | patch, MFA, segmentation |
| **Transfer** | Shift financial impact | cyber insurance, outsourcing with SLA |
| **Avoid** | Stop the activity | decommission the legacy service |
| **Accept** | Carry it, documented, with an owner and expiry | "known risk, compensating control in place" |

Acceptance must be *explicit, documented and time-boxed* — otherwise it is neglect.

## Lifecycle

Identify → analyse → evaluate (vs appetite) → treat → monitor/review. Standards: [[ISO 27001]] clause 6 (risk-based ISMS), [[NIST CSF]] (Identify), [[NIST 800-53]]/RMF (assess → authorise → monitor), [[CIS Controls]] (prioritised mitigations).

## Practical notes

- **CVSS is severity, not risk.** It ignores asset value, exposure and existing controls.
- Risk without an owner is a wish.
- Re-score after incidents and after major architecture changes.
- Concentration risk: 80% of revenue through one provider, one identity provider outage, one cloud region.
- Third-party/supply-chain risk is its own discipline ([[Supply Chain Attack]]).

## Related

- [[Vulnerability, Threat, Risk and Exploit]]
- [[Threat Modelling]]
- [[Security Controls]]
- [[Vulnerability Management]]
- [[Business Continuity and Disaster Recovery]]
- [[Foundations MOC]]
