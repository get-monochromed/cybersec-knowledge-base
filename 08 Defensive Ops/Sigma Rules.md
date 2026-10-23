---
title: Sigma Rules
aliases: [Sigma, SigmaHQ, Detection as Code]
category: defensive
tags: [defensive/detection, siem, tooling]
status: solid
up: "[[Defensive Ops MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: ["https://github.com/SigmaHQ/sigma"]
---

# Sigma Rules

## Summary

A vendor-neutral YAML format for describing log-based detections. Write once, convert to Splunk SPL, Elastic EQL, Microsoft Sentinel KQL, Wazuh, or CrowdStrike LogScale with `sigma-cli`. It is how detection engineering becomes version-controlled and reviewable instead of living in one analyst's SIEM tab.

## Anatomy

```yaml
title: Suspicious Shadow Copy Deletion
id: 1f2c3d4e-...
status: experimental
description: Shadow copies deleted outside backup tooling - common ransomware precursor.
references:
  - https://attack.mitre.org/techniques/T1490/
author: me
date: 2026/10/23
tags:
  - attack.impact
  - attack.t1490
logsource:
  product: windows
  service: process_creation
detection:
  selection:
    CommandLine|contains:
      - 'vssadmin delete shadows'
      - 'wmic shadowcopy delete'
      - 'vssadmin resize shadowstorage'
  condition: selection
falsepositives:
  - Backup software with unusual command lines
level: high
```

Key fields: `logsource` (which telemetry this needs), `detection` (named selections + a condition), `level` (informational → critical), `tags` ([[MITRE ATT&CK]] technique IDs), `falsepositives`.

## Workflow

1. Pick a technique — from intel, an incident, or ATT&CK coverage gaps ([[Purple Teaming]]).
2. Check SigmaHQ first; adapt rather than duplicate.
3. Write/test against real telemetry in a lab or via replay ([[Threat Hunting]]).
4. Convert: `sigma convert -t splunk -p windows rules/`.
5. Version in Git, review like code, and record the ATT&CK mapping.
6. Tune with the false positives you actually see; document suppressions.

## Why it helps

- **Portability** — swapping SIEM no longer means rewriting the detection library.
- **Review** — a YAML diff is reviewable; a GUI rule is not.
- **Coverage measurement** — tags map rules to ATT&CK, so you can count covered techniques.
- **Community** — thousands of maintained rules, including for cloud and Linux.

## Limits

- Only as good as the underlying telemetry: no `logsource`, no detection.
- Field names differ between products; conversions need correction.
- Behavioural detections often need multi-event correlation, which Sigma expresses awkwardly.
- Rules are a starting point, not a substitute for tuning against your environment.

## Related

- [[SIEM]]
- [[Purple Teaming]]
- [[Threat Hunting]]
- [[MITRE ATT&CK]]
- [[Defensive Ops MOC]]
