---
title: Threat Hunting
aliases: [Hunting, Hypothesis-Driven Hunting, Cyber Threat Hunting]
category: defensive
tags: [defensive/hunting, detection]
status: solid
up: "[[Defensive Ops MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Threat Hunting

## Summary

Proactively searching telemetry for evidence of compromise that existing detections missed. Not "looking at dashboards" — a hypothesis, a data-driven search, and a decision about what to do with the result.

## The loop

1. **Hypothesis** — a testable statement, ideally from intel, ATT&CK, or an incident.
2. **Data** — which sources would show it? Do you actually have them? Is retention long enough?
3. **Query/analysis** — statistical, behavioural, IOC sweep, or stack-counting.
4. **Triage** — findings become leads; leads become incidents or false positives.
5. **Output** — a new detection rule (that is the real deliverable), a data-source gap, or a control recommendation.

## Hypothesis sources

- **Intel-driven** — "this sector is being hit by group X using T1059.001 PowerShell download cradles" ([[Threat Intelligence]]).
- **ATT&CK-driven** — pick an uncovered technique, hunt it, then automate the detection.
- **Anomaly-driven** — stack-count rare parent-child process pairs, rare command lines, rare scheduled-task authors.
- **Incident-driven** — after every incident, hunt for the same activity elsewhere.
- **Situational** — new business acquisition, new cloud region, layoffs (insider risk).

## Example hypotheses

- "Attackers used legitimate remote-management tools (AnyDesk/ScreenConnect) to maintain access." → hunt install and connection events fleet-wide.
- "An account created a mailbox rule forwarding externally in the last 90 days."
- "A host made DNS requests to domains registered in the last 30 days."
- "A service was created shortly after a 4624 type 3 logon."

## Maturity

Level 0: relying on alerts. Level 1: IOC sweeps. Level 2: routine TTP hunts. Level 3: continuous, hypothesis-driven, integrated with detection engineering and purple teaming.

## Metrics

Hunts run, hypotheses validated, new detections produced, dwell time reduction, true positives found. "Hunts completed" alone is vanity.

## Related

- [[MITRE ATT&CK]]
- [[SIEM]]
- [[Purple Teaming]]
- [[Threat Intelligence]]
- [[Defensive Ops MOC]]
