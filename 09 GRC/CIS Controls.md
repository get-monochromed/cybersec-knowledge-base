---
title: CIS Controls
aliases: [CIS Critical Security Controls, CIS 18, CIS v8]
category: grc
tags: [grc/framework, cis, exam]
status: solid
up: "[[GRC MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: ["CIS Critical Security Controls v8.1"]
---

# CIS Controls

## Summary

A prioritised, prescriptive set of 18 safeguards, ordered by real-world effectiveness. The most actionable of the major frameworks: if you need a "what do we do first" list, this is it.

## Implementation groups

- **IG1** — basic hygiene, ~56 safeguards; every organisation. Blocks the majority of commodity attacks.
- **IG2** — mid-size with sensitive data; adds centralised management and monitoring.
- **IG3** — mature/high-value targets; adds advanced detection and defence in depth.

## The 18 controls (short form)

1. Inventory and control of enterprise assets
2. Inventory and control of software assets
3. Data protection
4. Secure configuration
5. Account management
6. Access control management
7. Continuous vulnerability management
8. Audit log management
9. Email and web browser protections
10. Malware defences
11. Data recovery
12. Network infrastructure management
13. Network monitoring and defence
14. Security awareness and skills training
15. Service provider management
16. Application software security
17. Incident response management
18. Penetration testing

## Why it works

- Ordering reflects evidence: asset/software inventory and patching stop more attacks than exotic controls. Most ransomware success maps to failures in controls 1, 4, 5, 7, 11.
- Each control has **safeguards** with concrete descriptions, and mappings to [[NIST CSF]] and [[ISO 27001]].
- Free **CIS Benchmarks** tell you how to configure specific products (very useful for [[Hardening]]).
- **CIS-CAT** scores hosts against the benchmarks.

## Using it

1. Pick your IG based on size and data sensitivity.
2. Assess current state per safeguard (implemented / partial / not).
3. Prioritise gaps that block multiple controls (inventory first — it is a prerequisite for everything).
4. Report progress as "% of safeguards implemented at IG1" — a genuinely useful board metric.

## Related

- [[NIST CSF]]
- [[ISO 27001]]
- [[Patch Management]]
- [[Vulnerability Management]]
- [[GRC MOC]]
