---
title: NIST SP 800-61
aliases: [NIST 800-61, Incident Handling Guide]
category: defensive
tags: [defensive/framework, nist]
status: developing
up: "[[Defensive Ops MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: ["NIST SP 800-61r2/r3"]
---

# NIST SP 800-61

## Summary

NIST's Computer Security Incident Handling Guide — the reference lifecycle for [[Incident Response]] and the source of the four-phase model taught almost everywhere.

## Phases

1. **Preparation**
2. **Detection and Analysis**
3. **Containment, Eradication and Recovery**
4. **Post-Incident Activity**

(Revision 3 reworks this toward a continuous "incident response lifecycle" aligned with [[NIST CSF]] 2.0 — Govern, Identify, Protect, Detect, Respond, Recover — but the four-phase structure remains the practical mental model.)

## What it specifies

- Building an IR capability: policy, plan, procedures, team structure, communication, and training.
- Incident handling detail per phase: evidence preservation, containment strategies, impact assessment, notification.
- Coordinating with external parties: CERTs, law enforcement, vendors, insurers.
- Metrics: time-based measures and the value of post-incident review.

## How to use it

- As the skeleton for your IR plan; adapt language to your organisation.
- Its incident-handling checklists make good tabletop exercise material.
- Pair with **NIST SP 800-86** (forensic techniques) and **SP 800-184** (recovery).

## Related

- [[Incident Response]]
- [[Digital Forensics]]
- [[NIST CSF]]
- [[Defensive Ops MOC]]
