---
title: Patch Management
aliases: [Patching, Update Management, Patch Cycle]
category: defence
tags: [defence/operations, hygiene]
status: solid
up: "[[Defences MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Patch Management

## Summary

Getting vendor fixes onto systems quickly and safely. Unpatched, internet-facing software is the most reliable way into a network — most ransomware still starts with a vulnerability that had a fix available for months.

## Process

1. **Inventory** — OS, firmware, applications, containers, appliances, libraries (SBOM). Include what scanning tends to miss: network gear, printers, hypervisors, OT.
2. **Assess** — map to KEV/EPSS, CVSS, exposure ([[Vulnerability Management]]).
3. **Prioritise** — internet-facing, exploit-in-the-wild, high-privilege systems first.
4. **Test** — pilot ring, then broad rollout; back out plan.
5. **Deploy** — automate (Intune, Ansible, WSUS/MECM, `dnf`/`apt` with unattended-upgrades).
6. **Verify** — scan again; report coverage, not just deployments.
7. **Handle exceptions** — compensating controls, owner, expiry date.

## Risk-based cadence (typical)

- **Emergency (24–72 h)**: actively exploited, internet-facing, or critical infrastructure.
- **Critical (7–14 days)**: high severity, exposed services.
- **Routine (30–90 days)**: everything else, including browsers and office suites.

## Hard parts

- **Legacy/EOL systems** with no vendor patch — isolate and compensate ([[Network Segmentation]]).
- **Downtime windows** and business resistance; solve with redundancy, not with delays.
- **Firmware and appliances** — often forgotten until a VPN CVE drops.
- **Third-party/OT** — vendor-controlled patching, certification cycles, no reboot allowed ([[OT and ICS Security]]).
- **Reboot avoidance culture** — `apt` patches that never apply because the kernel is not rebooted.

## Detect the gaps

- Agentless sweep of versions vs vendor advisories.
- Alert on hosts not reporting patch status for >7 days.
- Track "average age of unpatched criticals" as a board-level metric.

## Related

- [[Vulnerability Management]]
- [[Hardening]]
- [[CIS Controls]]
- [[Worm]]
- [[Defences MOC]]
