---
title: Threat Actor
aliases: [Adversary, Threat Agent, Attacker]
category: actor
tags: [actor/overview, exam]
status: solid
up: "[[Threats MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Threat Actor

## Summary

An individual or group that can act against a system. Defenders classify actors by **capability, intent, resources and access** because those predict the TTPs you will see — and therefore which controls and logs actually matter.

## Dimensions

- **Capability** — tooling, custom exploits, operational security discipline.
- **Intent / motivation** — financial, ideological, espionage, disruption, personal.
- **Resources** — funding, personnel, time, infrastructure, zero-days.
- **Access** — external only, supply chain, insider, physical.
- **Attribution** — how confidently you can name them (usually low; see false flags).

## Taxonomy

| Type | Capability | Typical goal |
|---|---|---|
| [[Script Kiddie]] | low | vandalism, kudos |
| [[Hacktivist]] | low–medium | publicity, ideology |
| [[Cybercriminal]] | medium–high | money (ransomware, fraud, data sale) |
| [[Insider Threat]] | legitimate access | theft, sabotage, revenge, negligence |
| [[Advanced Persistent Threat]] | very high | long-term access, espionage |
| [[Nation-State Actor]] | very high | strategic advantage, disruption |

Overlap is the norm: a nation-state rents initial access from criminals, or uses hacktivists as cover.

## Why classification matters

- Commodity crime is stopped by hygiene: patching, MFA, EDR, backups ([[CIS Controls]] top 5).
- APTs are not "stopped" by hygiene alone — they require detection depth, segmentation, identity hardening, and assumption of breach ([[Zero Trust Architecture]], [[Threat Hunting]]).
- Insiders defeat perimeter controls entirely; they need least privilege, monitoring of *authorised* actions, and [[Authentication, Authorization and Accounting|accounting]].

## Real-world naming

Vendors give intrusion sets names (APT29, Lazarus, FIN7, Volt Typhoon); MITRE uses G-numbers in [[MITRE ATT&CK]]; national CERTs attribute differently. Same actor, many names — map them, do not memorise the zoo.

## Related

- [[Threat Intelligence]]
- [[Indicators of Compromise]]
- [[Threat Modelling]]
- [[Risk Management]]
- [[Threats MOC]]
