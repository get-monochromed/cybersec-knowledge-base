---
title: OT and ICS Security
aliases: [OT Security, ICS Security, SCADA, Industrial Control Systems]
category: domain
tags: [domain/ot, critical-infrastructure]
status: developing
up: "[[Domains MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# OT and ICS Security

## Summary

Security of systems that control physical processes: SCADA, PLCs, RTUs, DCS, HMIs, safety instrumented systems. Priorities invert — **availability and safety come before confidentiality**, and a wrong packet can physically destroy equipment or hurt people.

## Key differences from IT

| IT | OT |
|---|---|
| Confidentiality first | Availability and safety first |
| Patch weekly | Patch on maintenance windows, sometimes never |
| Reboot freely | Reboot can stop a plant |
| Agents can be installed | Legacy OS, no agents, no AV |
| Network is untrusted | Network was air-gapped (until it wasn't) |
| Failure = downtime | Failure = physical damage |

## Purdue model (zones)

Level 0 process → 1 controllers → 2 supervisory (SCADA/HMI) → 3 operations (historians) → 3.5 DMZ → 4 enterprise → 5 internet. The DMZ between 3.5 and 4 is where IT/OT traffic is brokered; direct connections are the classic mistake.

## Threat model

- Nation-state pre-positioning ([[Nation-State Actor]]): Stuxnet, Industroyer, Triton (safety systems), Volt Typhoon.
- Ransomware that spreads from IT to OT — the most common real-world OT impact.
- Insiders and maintenance laptops carrying malware across the air gap.
- Legacy protocols (Modbus, DNP3, S7) with no authentication by design.

## Controls

- **Segmentation** with enforced conduits and a DMZ; no direct IT→OT paths ([[Network Segmentation]]).
- **Passive monitoring** — span/tap-based anomaly detection (Nozomi, Claroty, Dragos) because active scanning can crash legacy devices.
- **Asset inventory** without active probing; protocol-aware discovery.
- **Remote access** — jump host + MFA + session recording in the DMZ; no vendor direct VPN.
- **Change control** with safety review; test in a lab/staging PLC.
- **Backups of PLC logic and configurations** (offline), plus a recovery plan that accounts for physical restart sequences.
- **Physical security** and removable-media control.
- Standards: **IEC 62443**, NIST SP 800-82, NIS2 (EU).

## Detection

Protocol anomalies, unauthorised programming (PLC logic download), new devices on the OT network, engineering workstation talking to the internet.

## Related

- [[Network Segmentation]]
- [[Network Security]]
- [[Incident Response]]
- [[Domains MOC]]
