---
title: Network Segmentation
aliases: [Segmentation, Microsegmentation, VLAN, DMZ]
category: defence
tags: [defence/network, architecture]
status: solid
up: "[[Defences MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Network Segmentation

## Summary

Dividing the network into zones with controlled traffic between them, so compromise of one host does not grant reach to everything. The single most effective containment control against [[Worm|worms]], [[Ransomware]] and [[Lateral Movement]] — and the thing "flat networks" lack.

## Approaches

- **Physical** — separate switches/cabling; strongest, least flexible.
- **VLAN + routing/firewall** — classic zone model: user, server, DMZ, management, voice, IoT, OT.
- **Subnet-based ACLs** — coarse; cloud security groups/NACLs work this way.
- **Microsegmentation** — per-workload policy, often host-agent or service-mesh enforced (East-West traffic control). Workstations cannot talk to workstations.
- **Air gaps** — for OT/ICS or classified environments; broken by USB and vendor laptops more often than by network attacks.
- **Identity-based segmentation** — ZTNA/Zero Trust: policy by identity and device, not by IP ([[Zero Trust Architecture]]).

## Design pattern

1. Classify assets by sensitivity and function.
2. Define zones and the *only* allowed flows between them (documented, default deny).
3. Put a policy enforcement point between zones (firewall, security group, service mesh).
4. Force admin traffic through a management zone / jump host (PAW).
5. Monitor inter-zone traffic — unusual crossings are high-fidelity alerts.

## What it buys you

- Ransomware cannot reach backups if backups are in a separate zone with pull-only access.
- Domain controllers unreachable from user VLANs except via admin paths.
- OT cannot be reached from the corporate LAN.
- Blast radius becomes measurable rather than theoretical.

## Pitfalls

- "Segmented" diagrams that do not match the firewall rules.
- Emergency `any` rules added during an incident and never removed.
- Over-segmentation without automation — operationally unmaintainable.
- Assuming VLAN = security boundary when routing permits everything.
- Ignoring identity: an attacker with domain admin can cross zones legitimately ([[Privilege Escalation]]).

## Related

- [[Firewall]]
- [[Zero Trust Architecture]]
- [[Lateral Movement]]
- [[OT and ICS Security]]
- [[Defences MOC]]
