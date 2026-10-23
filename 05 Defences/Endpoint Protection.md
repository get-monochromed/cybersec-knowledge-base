---
title: Endpoint Protection
aliases: [EDR, XDR, Antivirus, Endpoint Security, EPP]
category: defence
tags: [defence/endpoint, detection]
status: solid
up: "[[Defences MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Endpoint Protection

## Summary

Software on the host that prevents, detects and responds to malicious behaviour. The modern stack is EDR (detection and response with telemetry) inside an EPP platform, feeding XDR correlation — with classic AV as one component, not the product.

## Layers

- **AV / EPP** — prevention: signatures, heuristics, exploit mitigation, device control, firewall, web filtering.
- **EDR** — continuous telemetry (process, file, registry, network, memory), behavioural detection, and response actions (isolate host, kill process, quarantine, roll back).
- **XDR** — EDR + identity + email + cloud + network signals correlated in one platform.
- **MDR** — the same as a managed service, for teams without 24/7 staff.

## What good looks like

- **Behaviour-based detections**, not just file hashes ([[Antivirus Detection Techniques]]).
- **Tamper protection** — an attacker's first move is disabling the agent; alert if it stops reporting.
- **Full command-line and script-block telemetry** (essential for [[Living off the Land]], [[Fileless Malware]]).
- **Response actions tested** — isolation actually works through the firewall/VLAN.
- **Detection content reviewed** against [[MITRE ATT&CK]] coverage; tune noise aggressively.
- **Offline/isolated hosts** still covered (agent health is a control in itself).

## Operational realities

- EDR is a data firehose: without [[SIEM]] correlation and a triage process it becomes expensive noise.
- Coverage gaps: OT/ICS, legacy OS, mobile, containers (agentless scanning), cloud workloads.
- An agent with SYSTEM privileges is itself an attack surface; keep it patched.
- Alert on **agent disabled / uninstalled**, not just on detections — that is usually the real signal.

## Related

- [[Antivirus Detection Techniques]]
- [[Malware Analysis]]
- [[SIEM]]
- [[Incident Response]]
- [[Threat Hunting]]
- [[Defences MOC]]
