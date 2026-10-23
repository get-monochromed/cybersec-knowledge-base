---
title: Pyramid of Pain
aliases: [Pyramid of Pain]
category: actor
tags: [actor/intel, detection, exam]
status: developing
up: "[[Threats MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: ["Bianco, Enterprise Detection & Response"]
---

# Pyramid of Pain

## Summary

David Bianco's model of how much *pain* each type of indicator causes an adversary when you detect and block it. Bottom = trivial to change; top = forces the attacker to relearn behaviour.

## The pyramid, bottom to top

1. **Hash values** — one byte changes, defeated. Zero pain.
2. **IP addresses** — rotate infrastructure trivially.
3. **Domain names** — cheap to re-register, small friction.
4. **Network/host artefacts** — user-agents, registry keys, mutexes, named pipes; moderate friction.
5. **Tools** — the malware or utility itself. Blocking it forces the attacker to use something else (real pain).
6. **TTPs** (tactics, techniques, procedures) — how they operate. Detecting the behaviour forces retraining and redesign.
7. **"Tough!"** — the apex: detection so attuned to the actor's habits that they must fundamentally change.

## Why it matters

- Explains why IOC blocklists feel productive but change little.
- Argues for detection engineering on [[MITRE ATT&CK]] techniques, not indicator feeds.
- Sets a maturity ladder: IOC-based detection → tool-based → behaviour-based.
- Guides [[Threat Hunting]] hypotheses toward the top of the pyramid.

## Caveat

Detection cost also rises with the pyramid: TTP detections need quality telemetry and tuning, and broad behaviour rules can create false positives. The art is the middle: detect tools and artefacts while building TTP coverage where the actor matters.

## Related

- [[Indicators of Compromise]]
- [[Threat Intelligence]]
- [[MITRE ATT&CK]]
- [[Threat Hunting]]
- [[Threats MOC]]
