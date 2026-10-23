---
title: Penetration Testing
aliases: [Pentest, Pen Test, Ethical Hacking Assessment]
category: offensive
tags: [offensive/pentest, exam]
status: solid
up: "[[Offensive MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Penetration Testing

## Summary

A time-boxed, authorised, goal-directed attack simulation against a defined scope, producing evidence and remediation advice. It is assurance, not a security programme: a point-in-time sample, not proof of safety.

## Types

- **Black box** — no prior knowledge; simulates an external attacker; slow, realistic.
- **Grey box** — some credentials/architecture provided; best value for most engagements.
- **White box** — full knowledge and source access; deepest coverage, least realistic.
- **External / internal / web app / mobile / cloud / wireless / physical / social engineering** — scope variants.
- **Red team** — objective-based, stealth-focused ([[Red Teaming]]).
- **Continuous / automated** — BAS, DAST, bug bounty ([[Bug Bounty]]).

## Phases (PTES-style)

1. Pre-engagement — [[Rules of Engagement]], scope, contacts, emergency stop.
2. [[Reconnaissance]] · 3. [[Scanning and Enumeration]] · 4. [[Exploitation]] · 5. [[Post Exploitation]].
6. Reporting — executive summary, findings with evidence and severity, remediation, attack narrative.
7. Retest — verify fixes.

## Reporting quality

The report is the deliverable. Good findings have: what, where, proof (request/response, screenshot), impact in business terms, severity with justification (CVSS + context), and a specific fix. "Critical: outdated TLS" with no exploitability argument wastes the client's money.

Severity framing: CVSS base score + environmental context (exposure, data sensitivity, compensating controls) — see [[Risk Management]].

## Limits

- Samples a moment in time; a clean pentest is not a clean bill of health.
- Scope misses are common: third parties, cloud IAM, people, processes.
- Pentesters and real attackers optimise differently — stealth and persistence are under-tested in a standard engagement.
- Without retesting, findings are just documents.

## Related

- [[Red Teaming]]
- [[Purple Teaming]]
- [[Vulnerability Management]]
- [[Rules of Engagement]]
- [[Offensive MOC]]
