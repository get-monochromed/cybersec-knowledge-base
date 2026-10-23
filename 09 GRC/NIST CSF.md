---
title: NIST CSF
aliases: [Cybersecurity Framework, NIST CSF 2.0, CSF]
category: grc
tags: [grc/framework, nist, exam]
status: solid
up: "[[GRC MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: ["NIST CSF 2.0 (2024)"]
---

# NIST CSF

## Summary

A voluntary, outcome-based framework for structuring a security programme. It does not tell you which controls to implement — it tells you the functions a programme must cover, so you can map whatever standards and tools you already use.

## 2.0 functions (six)

1. **Govern** — strategy, roles, policy, risk appetite, supply-chain risk. *(New in 2.0; sits across the others.)*
2. **Identify** — asset management, risk assessment, improvement.
3. **Protect** — identity, access, training, data security, platform security, resilience.
4. **Detect** — continuous monitoring, adverse event analysis.
5. **Respond** — response planning, communication, mitigation, improvement.
6. **Recover** — recovery planning, communication, improvement.

Each function breaks into **categories** and **subcategories** (outcomes), e.g. `PR.AA-05` "access permissions are managed, incorporating least privilege".

## Implementation tiers

1. Partial (ad hoc) → 2. Risk-informed → 3. Repeatable → 4. Adaptive. Tiers describe governance maturity, not technical sophistication — a company can be Tier 3 with modest tooling.

## Profiles

- **Current profile** — outcomes achieved today.
- **Target profile** — where you need to be, given risk appetite.
- The gap becomes the roadmap. This is the most practical use of the framework.

## How to use it

- Map existing controls/standards to subcategories (informative references exist for ISO 27001, 800-53, CIS).
- Report to the board in CSF language — it is designed to be readable by non-specialists.
- Do not treat it as a checklist to "complete"; the value is the gap analysis and prioritisation.

## Related

- [[ISO 27001]]
- [[NIST 800-53]]
- [[CIS Controls]]
- [[Risk Management]]
- [[GRC MOC]]
