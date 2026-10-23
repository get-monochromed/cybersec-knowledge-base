---
title: Security Operations Centre
aliases: [SOC, Blue Team, Security Operations]
category: defensive
tags: [defensive/soc, operations]
status: solid
up: "[[Defensive Ops MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Security Operations Centre

## Summary

The team and process that monitors, triages and responds to security events, 24/7 in mature organisations. Technology is the easy part; the hard parts are alert quality, escalation decisions, and not burning out analysts.

## Tiers

- **Tier 1** — triage alerts against runbooks, close false positives, escalate.
- **Tier 2** — investigate, correlate across data sources, contain, communicate.
- **Tier 3 / threat hunter** — deep investigation, hunting, detection engineering, malware analysis.
- **Detection engineering** — owns the rule set and its quality (often separate in mature SOCs).
- **SOC manager** — staffing, metrics, stakeholder reporting.
- **IR team** — may be separate; takes over major incidents.

**Common misconception:** Tier 1 does not "do malware analysis all day", and Tier 3 does not "just close tickets". Tier 1 triages against runbooks and escalates; Tier 2 investigates and contains; Tier 3 hunts, does DFIR and malware analysis, and writes detections. In small teams one person wears all three hats — the tier names describe *decisions*, not seniority.

## Workflow

Alert → triage (is it real? is it in scope? what is the impact?) → enrich (asset, identity, intel) → escalate or close → contain/eradicate/recover → document → lessons learned → detection improvement.

## Metrics

- **MTTD** — mean time to detect.
- **MTTA** — time to acknowledge; **MTTR** — time to resolve/contain.
- **Dwell time** — how long an attacker was present before detection (the number that matters most).
- **False positive rate** — high FP rate is the main cause of alert fatigue.
- **Coverage** — techniques with working detections ([[MITRE ATT&CK]]).

## Model choice

- **In-house 24/7** — expensive, full control.
- **Follow-the-sun** across regions — best for global firms.
- **MDR / co-managed** — outsourced triage with in-house escalation; common for mid-size.
- **8×5 in-house + on-call** — realistic for many organisations; document the gap.

## Failure modes

- Alert volume over alert quality; analysts click "close" without investigating.
- No runbooks, so every analyst improvises.
- SIEM content never tuned after deployment.
- No feedback loop from IR back into detection ([[Purple Teaming]] fixes this).
- Treating the SOC as a CCTV operator rather than an investigative function.

## Related

- [[SIEM]]
- [[SOAR]]
- [[Incident Response]]
- [[Threat Hunting]]
- [[Defensive Ops MOC]]
