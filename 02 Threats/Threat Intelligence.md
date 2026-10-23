---
title: Threat Intelligence
aliases: [CTI, Cyber Threat Intelligence, TI]
category: actor
tags: [actor/intel, defensive]
status: solid
up: "[[Threats MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Threat Intelligence

## Summary

Evidence-based knowledge about adversaries — who they are, what they do, what they use — turned into decisions. If it does not change a decision (patch this, hunt for that, block this), it is news, not intelligence.

## Levels

| Level | Audience | Question | Example |
|---|---|---|---|
| **Strategic** | executives | What threats matter to the business? | sector-targeting ransomware surge |
| **Operational** | security managers | Who is coming and how? | a group's campaign against our industry |
| **Tactical** | SOC analysts | What do we detect? | TTPs, [[MITRE ATT&CK]] mappings |
| **Technical** | tools/automation | What do we block? | hashes, IPs, domains ([[Indicators of Compromise]]) |

## The intelligence cycle

Requirements → collection → processing → analysis → dissemination → feedback. Requirements matter most: "tell me everything" produces noise.

## Sources

- **OSINT** — vendor blogs, CERT advisories (CISA KEV), MITRE ATT&CK, research reports, social media.
- **Commercial feeds** — paid, often largely IOC lists; evaluate precision.
- **ISACs / sector sharing** — e.g. FS-ISAC; the most useful in practice.
- **Dark web / underground monitoring** — credential dumps, broker posts.
- **Internal telemetry** — the best intel is what happened to *you* ([[SIEM]], [[Incident Response]] findings).

## Feeds vs TTPs

Feeds of IPs and hashes decay fast (attacker rotates infrastructure) and are trivially evaded. Behavioural intelligence mapped to ATT&CK is durable: "this group uses `rundll32` to proxy execution" survives infrastructure changes. This is the **[[Pyramid of Pain]]** argument — IOCs hurt the analyst, not the adversary; TTPs hurt the adversary.

## Making it operational

- Enrich alerts with intel (context, actor, campaign) instead of adding more blocklists.
- Track campaigns, not individual IOCs.
- Measure: intel that produces no detection, hunting hypothesis or decision is cost.
- Sharing has legal/PII constraints — anonymise where needed.

## Related

- [[Indicators of Compromise]]
- [[Pyramid of Pain]]
- [[MITRE ATT&CK]]
- [[Threat Hunting]]
- [[Threats MOC]]
