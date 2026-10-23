---
title: MITRE ATT&CK
aliases: [ATT&CK, MITRE ATTACK, ATT&CK Framework]
category: defensive
tags: [defensive/framework, mitre, exam]
status: solid
up: "[[Defensive Ops MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: ["https://attack.mitre.org"]
---

# MITRE ATT&CK

## Summary

A curated knowledge base of adversary **tactics, techniques and procedures** observed in the real world. The de facto common language linking threat intelligence, detection engineering, red teaming and control coverage. Replaced the [[Cyber Kill Chain]] as the granular model.

## Structure

- **Tactics** (the "why") — 14 columns: Reconnaissance, Resource Development, Initial Access, Execution, Persistence, Privilege Escalation, Defense Evasion, Credential Access, Discovery, Lateral Movement, Collection, Command and Control, Exfiltration, Impact.
- **Techniques** (the "how") — e.g. T1566 Phishing, T1059 Command and Scripting Interpreter, T1003 OS Credential Dumping. Techniques have **sub-techniques** (`T1003.001` LSASS Memory).
- **Procedures** — specific implementations by specific actors.
- **Groups** (G-numbers, intrusion sets) and **Software** (S-numbers) — attribution and tooling.
- **Mitigations** (M-numbers) and **Data Sources/Components** — what telemetry detects each technique.

Three matrices: **Enterprise** (Windows/macOS/Linux/Cloud/Network/Containers), **Mobile**, **ICS**.

## How each team uses it

- **Intel** — describe an actor's TTPs, compare campaigns.
- **Detection** — build rules per technique; track coverage in **ATT&CK Navigator** heatmaps ([[Purple Teaming]]).
- **Red team** — plan emulation by tactic ([[Red Teaming]]).
- **Defence** — map controls to techniques they disrupt; justify investment ([[Risk Management]]).
- **Hunting** — hypotheses derived from a technique ([[Threat Hunting]]).

## Limits

- Descriptive, not prescriptive — it tells you what happens, not what to buy.
- Coverage gaps: it does not model business-logic abuse or many cloud-identity nuances well.
- Techniques are broad; a "covered" technique may be detected only for one sub-case.
- ATT&CK IDs change over time; version your mappings.

## Related

- [[Cyber Kill Chain]]
- [[Threat Intelligence]]
- [[Threat Hunting]]
- [[Purple Teaming]]
- [[Defensive Ops MOC]]
