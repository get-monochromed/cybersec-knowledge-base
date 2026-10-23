---
title: Purple Teaming
aliases: [Purple Team, Detection Engineering Collaboration]
category: offensive
tags: [offensive/purple, detection]
status: solid
up: "[[Offensive MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Purple Teaming

## Summary

Red and blue working together, on purpose: execute an attack technique, see whether it is detected, then build or fix the detection immediately. It converts offensive findings into defensive coverage instead of a PDF.

## Loop

1. Pick a technique from [[MITRE ATT&CK]] (ideally one used by a relevant [[Threat Actor]]).
2. Execute it (Atomic Red Team, Caldera, manual, or the red team's emulation plan).
3. Observe: did telemetry capture it? Did a rule fire? How long until triage?
4. Fix: add data source, write/adjust the detection rule (Sigma → [[SIEM]]), tune false positives.
5. Re-run and record coverage.

## What it produces

- **Detection coverage map** — ATT&CK heatmap of tested, detected, blind.
- **Detection-as-code** — versioned Sigma/YARA/EDR rules with tests.
- **Honest metrics** — "% of targeted techniques detected" is a real control metric; "we have EDR" is not.

## Data prerequisites

No telemetry, no purple team. Minimum: process command lines, script block logging, authentication events, DNS, proxy, cloud audit logs, EDR behavioural events. See [[SIEM]].

## Common findings

- Technique works and nothing logs it (data source missing — the expensive fix).
- Logged but no rule (cheap fix: write the rule).
- Rule exists but is too noisy and muted (tuning problem).
- Alert fires but triage ignores it (process problem — the most common real-world failure).

## Tooling

Atomic Red Team, MITRE Caldera, Stratus Red Team (cloud), Infection Monkey, Sigma + `sigma-cli`, DetectionLab-style test environments.

## Related

- [[MITRE ATT&CK]]
- [[Red Teaming]]
- [[Threat Hunting]]
- [[Security Operations Centre]]
- [[Offensive MOC]]
