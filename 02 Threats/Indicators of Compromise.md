---
title: Indicators of Compromise
aliases: [IOC, IOCs]
category: actor
tags: [actor/intel, detection]
status: solid
up: "[[Threats MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Indicators of Compromise

## Summary

Observable artefacts that suggest an intrusion: file hashes, IPs, domains, URLs, registry keys, mutexes, user-agent strings, TLS certificate fingerprints, named pipes, email sender patterns. Useful for detection and retro-hunting, weak as durable knowledge.

## Types

- **Atomic** — single observable: hash, IP, domain.
- **Computed** — derived from a family: regex for a URI pattern, YARA rule ([[Malware Analysis]]).
- **Behavioural** — sequences: `rundll32` spawning from `winword.exe`, encoded PowerShell with `-nop -w hidden`, scheduled task created immediately after login.
- **Host vs network** — process/registry/file artefacts vs DNS/HTTP/flow artefacts.

## Strengths and weaknesses

| Strengths | Weaknesses |
|---|---|
| Cheap to share and automate | Trivially changed by attackers |
| Good for retro-hunting past traffic | Prone to false positives (CDN IPs, shared hosting) |
| Concrete enough for blocklists | Rapidly stale; high volume, low signal |

A known IOC tells you an attack *already happened*. Treat detection of an IOC as confirmation, not prevention.

## Using them well

1. **Retro-hunt**: search historical telemetry (proxy, [[SIEM]], EDR) for the IOC to find earlier victims.
2. **Enrich, don't block blindly** — check freshness, prevalence, and whether blocking breaks business traffic.
3. **Pivot to behaviour**: from an IOC, derive the TTP, and hunt the TTP ([[Threat Hunting]]).
4. **Automate expiry** — feeds age; expire IOCs after N days unless re-confirmed.
5. **Share** with sector ISACs where permitted.

## Where they come from

[[Threat Intelligence]] feeds, vendor reports, CERT advisories, sandbox output ([[Malware Analysis]]), and your own incidents — the last is the highest quality.

## Related

- [[Threat Intelligence]]
- [[Pyramid of Pain]]
- [[Malware Analysis]]
- [[Threat Hunting]]
- [[Threats MOC]]
