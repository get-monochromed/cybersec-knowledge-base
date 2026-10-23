---
title: Cyber Kill Chain
aliases: [Kill Chain, Lockheed Martin Kill Chain]
category: attack
tags: [attack/overview, framework, exam]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: ["Lockheed Martin, Intelligence-Driven Computer Network Defense (2011)"]
---

# Cyber Kill Chain

## Summary

Lockheed Martin's seven-stage model of an intrusion, borrowed from military targeting. Its value is that each stage is an opportunity to detect or interrupt — the earlier, the cheaper.

## Stages

1. **Reconnaissance** — target selection, OSINT, scanning ([[Reconnaissance]]).
2. **Weaponisation** — build the deliverable: malicious document, exploit, implant.
3. **Delivery** — transmit it: email, USB, watering hole, exposed service ([[Phishing]], [[Supply Chain Attack]]).
4. **Exploitation** — trigger the vulnerability or the user's action ([[Exploitation]]).
5. **Installation** — establish persistence: service, scheduled task, registry, implant ([[Post Exploitation]]).
6. **Command and Control (C2)** — outbound channel to the operator (DNS, HTTPS, cloud services).
7. **Actions on Objectives** — the actual goal: exfiltration, encryption, destruction, fraud.

## Why defenders like it

- Maps neatly to controls: block delivery (mail filter), detect exploitation (EDR), break C2 (egress filtering/[[DNS Attacks|DNS monitoring]]) — each break resets the attacker's work.
- Gives non-technical stakeholders a mental model and a common vocabulary.
- Emphasises that **intrusions are processes**, not single events.

## Limitations

- Assumes a perimeter-focused, malware-centric intrusion. Cloud identity attacks, insider threats and supply-chain compromises do not fit the linear flow.
- Weak for detecting *already-established* adversaries — it describes the initial chain, not post-compromise dwell.
- Coarse: "exploitation" covers hundreds of distinct techniques.

That is why [[MITRE ATT&CK]] (14 tactics, ~200 techniques, per-platform) replaced it for detection engineering, while the kill chain remains useful for communication and control mapping.

## Relationship to ATT&CK

| Kill chain | Nearest ATT&CK tactics |
|---|---|
| Reconnaissance | Reconnaissance, Resource Development |
| Weaponisation/Delivery | Initial Access |
| Exploitation | Execution, Privilege Escalation |
| Installation | Persistence |
| C2 | Command and Control |
| Actions | Collection, Exfiltration, Impact |

## Related

- [[MITRE ATT&CK]]
- [[Attack Taxonomy]]
- [[Threat Modelling]]
- [[Defence in Depth]]
- [[Attacks MOC]]
