---
title: Cyber Insurance
aliases: [Cyber Liability Insurance, Cyber Cover, Act of War Exclusion]
category: grc
tags: [grc/risk, insurance, incident]
status: developing
up: "[[GRC MOC]]"
created: 2026-10-24
updated: 2026-10-24
sources: ["Wikipedia: Petya (malware family) (clipping, ingested 2026-10-24)"]
---

# Cyber Insurance

## Summary

A transfer mechanism: pay a premium, shift part of the financial impact of an incident to an insurer. It is [[Risk Management]]'s **transfer** option applied to cyber, and it is the only control in the estate whose terms are negotiated by lawyers rather than engineers.

The reason it deserves its own note is [[NotPetya]]. Mondelez's insurer refused a US$100 million claim on the grounds that a state-backed attack was an **"act of war"** excluded by the policy — a dispute that went to litigation and settled confidentially in 2022. Every cyber policy written since has been shaped by that argument.

## What is actually insured

| Cover | What it pays for |
|---|---|
| **First party** | Incident response costs, forensics, legal, notification, credit monitoring, business interruption, data restoration, ransom (where lawful) |
| **Third party** | Defence costs, settlements and judgments from customer/consumer claims, regulatory fines where insurable |
| **Crisis management** | PR, call-centre, negotiation support |

Two structural features decide whether the policy is worth anything:

- **Aggregation** — one event hitting many insureds (a cloud provider outage, a widely used SaaS compromise) can exhaust a single limit or trigger one deductible across a group.
- **Silent cyber** — cyber exposure sitting unmentioned inside property, D&O or general liability policies. Insurers have been adding explicit exclusions to remove it, which quietly reduces cover organisations believed they had.

## Exclusions to read line by line

- **Act of war / hostile state action** — the NotPetya test. Wording matters enormously: "war" as declared war, or "warlike action by a military force", or "state-sponsored cyber operation"? Attribution is the insurer's burden in principle, but proving it is the insured's problem in practice.
- **Failure to maintain minimum controls** — many policies now condition cover on MFA, offline backups, EDR, patch SLAs. The insurer is doing [[Security Controls]] underwriting.
- **Prior known acts / failure to disclose** on the application. A mis-stated control can void the claim.
- **Systemic / infrastructure failure**, contractual fines, and (in some jurisdictions) regulatory penalties.
- **Ransom payments** — legally restricted or prohibited in some jurisdictions, and a sanctions question regardless of the policy.

## Making it useful

1. **Price the interruption, not just the breach** — model downtime in revenue terms ([[Business Continuity and Disaster Recovery]]). Under-insuring BI is the common error.
2. **Align the policy with the actual controls** — if the application says MFA everywhere, MFA everywhere is a claim condition ([[Authentication, Authorization and Accounting]]).
3. **Pre-agree the panel** — insurers' incident response vendors, retainer terms and notification deadlines. Finding this out during an incident wastes the window ([[Incident Response]]).
4. **Keep it as a layer, not a strategy** — insurance pays money after the fact; it does not restore availability, reputation or customer trust ([[Backup and Recovery]]).
5. **Read alongside contracts** — indemnity clauses and SLAs decide who pays before the insurer does.

> [!warning] Unverified — policy-market detail
> The source clipping establishes only one fact: Zurich American refused Mondelez's NotPetya claim as an act of war, Mondelez sued for US$100 million in 2018, and the suit settled in 2022 with confidential terms. The broader market behaviour described here (silent cyber exclusions, control-conditioned cover, war/state-backed exclusion tightening) is general background, not sourced from the clipping — verify against current policy wordings.

## Related

- [[Risk Management]]
- [[NotPetya]]
- [[Business Continuity and Disaster Recovery]]
- [[Ransomware]]
- [[Incident Response]]
- [[GRC MOC]]
