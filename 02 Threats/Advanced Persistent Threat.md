---
title: Advanced Persistent Threat
aliases: [APT, APT Group, Intrusion Set]
category: actor
tags: [actor/apt, mitre]
status: solid
up: "[[Threats MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Advanced Persistent Threat

## Summary

An intrusion set that combines high capability, stealth and patience to maintain long-term access to a specific target. "Advanced" means custom tooling and disciplined OPSEC; "persistent" means they intend to stay for months or years, not that they are noisy.

## Characteristics

- **Targeted** — chosen for strategic value, not opportunism.
- **Long dwell time** — weeks to years; measured in intrusions, not incidents.
- **Low and slow** — living off the land, valid accounts, minimal custom malware on disk.
- **Resourced** — teams, funding, infrastructure rotation, sometimes zero-days.
- **Goal-driven** — espionage, intellectual property, pre-positioning for disruption.

Often state-sponsored or state-tolerant ([[Nation-State Actor]]), but the label describes behaviour, not sponsor. MITRE tracks them as *intrusion sets* (G-numbers) in [[MITRE ATT&CK]]; vendors use their own names (APT29/Cozy Bear, APT28/Fancy Bear, Lazarus, Volt Typhoon). Same actor, many aliases — map, don't memorise.

## Lifecycle (typical)

1. **Reconnaissance** — target selection, OSINT on people and suppliers.
2. **Initial access** — spear [[Phishing]], valid credentials, edge-device exploitation, [[Supply Chain Attack]].
3. **Establishment** — persistence, C2 channel, credential dumping ([[Post Exploitation]]).
4. **Privilege escalation & lateral movement** — toward domain admin, cloud control plane, or the data itself.
5. **Collection & exfiltration** — staged, encrypted, often over legitimate cloud services.
6. **Persistence/maintenance** — quiet access, sometimes dormant for a future operation.
7. **Impact** — rarely; for APTs data is the prize, destruction is a separate mission (wiper attacks).

## Why hygiene is not enough

Patching and AV remove commodity threats, but an APT with a novel technique or valid credentials bypasses both. Defence requires:

- **Assume breach**: segmentation, [[Zero Trust Architecture]], least privilege, credential hygiene.
- **Detection depth**: [[Threat Hunting]] for ATT&CK techniques rather than IOCs, EDR telemetry, identity analytics.
- **Supply-chain assurance** and vendor access control.
- **Intelligence-led defence**: [[Threat Intelligence]] on the specific groups that care about your sector.

## Related

- [[Nation-State Actor]]
- [[Cyber Kill Chain]]
- [[MITRE ATT&CK]]
- [[Living off the Land]]
- [[Threat Hunting]]
- [[Threats MOC]]
