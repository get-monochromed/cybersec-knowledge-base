---
title: Red Teaming
aliases: [Red Team, Adversary Emulation, Adversary Simulation]
category: offensive
tags: [offensive/redteam]
status: solid
up: "[[Offensive MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Red Teaming

## Summary

Objective-driven adversary emulation: can a realistic attacker achieve a specific goal (access the crown-jewel database, get domain admin, reach the OT network) without being detected? It tests people, process, detection and response — not just vulnerabilities.

## Pentest vs red team

| | [[Penetration Testing]] | Red Teaming |
|---|---|---|
| Goal | find as many vulnerabilities as possible | achieve a specific objective |
| Stealth | not required | core requirement |
| Scope | broad list of assets | paths, not assets |
| Duration | days to weeks | weeks to months |
| Detection | usually known to defenders | usually covert; blue team unaware |
| Output | findings list | attack narrative + detection gaps |

## Process

1. **Objective** defined by the client (e.g. "obtain 100 customer records").
2. **Threat intelligence** — which adversary is realistic for this client ([[Threat Intelligence]], [[MITRE ATT&CK]]).
3. **Emulation plan** — TTPs mapped to ATT&CK, infrastructure, OPSEC.
4. **Execution** — initial access (often [[Phishing]] or a physical/USB vector), C2, privesc, movement, objective.
5. **Deconfliction** — a trusted white cell knows the plan, so incident response does not tear down the exercise.
6. **Reporting** — attack path, dwell time, what was detected and when, detection engineering recommendations.

## Infrastructure and OPSEC

Redirectors, domain categorisation, TLS certificates, beacon profiles, evasion of EDR — all designed to look like the emulated adversary. Blue teams should be told *after*, not during.

## Value

- Tests detection and response, which pentests do not.
- Produces concrete detection engineering work for [[Purple Teaming]].
- Exposes process gaps (helpdesk, physical security, third-party trust) that scanners never see.

## Related

- [[Purple Teaming]]
- [[Penetration Testing]]
- [[MITRE ATT&CK]]
- [[Threat Hunting]]
- [[Offensive MOC]]
