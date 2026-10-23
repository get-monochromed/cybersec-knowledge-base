---
title: Threat Modelling
aliases: [Threat Modeling, STRIDE, Threat Model]
category: foundation
tags: [foundation/core, threat-modelling, design]
status: solid
up: "[[Foundations MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Threat Modelling

## Summary

Structured "what can go wrong here?" done at design time, when changes are cheap. Output is a list of threats with owners and mitigations, not a document that gets filed and forgotten.

## The four questions (Shostack)

1. What are we building? — diagram: components, data flows, [[Trust Boundaries]].
2. What can go wrong? — enumerate threats per element/boundary.
3. What are we going to do about it? — mitigate, eliminate, transfer, accept ([[Risk Management]]).
4. Did we do a good job? — review, test, retest.

## Methodologies

### STRIDE (per element / boundary)
| Letter | Threat | Violates | Example |
|---|---|---|---|
| **S**poofing | Impersonating an identity | Authentication | stolen session cookie ([[Session Hijacking]]) |
| **T**ampering | Modifying data or code | Integrity | parameter tampering, MITM edit ([[Man-in-the-Middle (MITM)]]) |
| **R**epudiation | Denying an action | Non-repudiation | no audit log ([[Authentication, Authorization and Accounting\|AAA]]) |
| **I**nformation disclosure | Leaking data | Confidentiality | verbose errors, S3 bucket open |
| **D**enial of service | Degrading availability | Availability | [[Denial of Service (DoS)]] |
| **E**levation of privilege | Gaining rights | Authorization | [[Privilege Escalation]] |

STRIDE works best paired with data-flow diagrams — apply the relevant letters to each process, data store, data flow and boundary crossing.

### Others
- **DREAD** — Damage, Reproducibility, Exploitability, Affected users, Discoverability: scoring, largely superseded by CVSS + risk.
- **Attack trees** — root = attacker goal, children = sub-goals (AND/OR). Good for focused "how would they do X".
- **PASTA** — 7-stage, risk-centric, business-aligned; heavier, used in enterprise.
- **LINDDUN** — privacy threats (linkability, identifiability, non-repudiation, detectability, disclosure, unawareness, non-compliance).
- **Kill chain / [[MITRE ATT&CK]]** — defender-side enumeration of what the adversary does next; ATT&CK is effectively a threat library for step 2.
- **VAST**, **OCTAVE**, **Trike** — enterprise variants; know they exist.

## Operational tips

- Model new features, not just new systems; a new API endpoint is a new boundary.
- Model the **attacker with the most to gain**, not the average one ([[Threat Actor]]).
- Include abuse cases: "user submits someone else's ID", "admin goes rogue" ([[Insider Threat]]).
- Track threats like bugs: ID, description, STRIDE class, severity, mitigation, owner, status.
- Revisit after incidents — every real incident was a missed or mis-scored threat.

## Related

- [[Trust Boundaries]]
- [[Attack Surface]]
- [[Risk Management]]
- [[MITRE ATT&CK]]
- [[Vulnerability, Threat, Risk and Exploit]]
- [[Foundations MOC]]
