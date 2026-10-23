---
title: IDS and IPS
aliases: [IDS, IPS, Intrusion Detection System, Intrusion Prevention System, NIDS, HIDS]
category: defence
tags: [defence/detection, network]
status: solid
up: "[[Defences MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# IDS and IPS

## Summary

Detection (IDS) and in-line blocking (IPS) of malicious network or host activity using signatures, anomaly models or policy. Detection is the foundation of everything in [[Defensive Ops MOC|defensive operations]]; prevention is a bonus with an availability cost.

## Flavours

| Type | Position | Sees |
|---|---|---|
| **NIDS** | network tap/SPAN | packets, flows (Snort, Suricata, Zeek) |
| **NIPS** | inline | can drop packets; latency and false-positive risk |
| **HIDS** | on host | file integrity, logs, process behaviour (OSSEC, Wazuh) |
| **HIPS/EDR** | on host, behavioural | process trees, memory, syscalls ([[Endpoint Protection]]) |
| **WIDS** | wireless | rogue APs, deauth floods |

## Detection methods

- **Signature** — pattern match on traffic (exploit strings, C2 user agents). Precise for known attacks, blind to new ones.
- **Anomaly** — deviation from a baseline; catches novel activity, generates noise.
- **Protocol/state analysis** — malformed packets, RFC violations, tunnelling.
- **Reputation/intel feeds** — known-bad IPs/domains (decays fast; see [[Pyramid of Pain]]).
- **Policy** — "this should never happen" rules (e.g. SMB from a workstation to the internet).

## Operating them

- **Tuning is the job**: baseline, suppress known-good noise, then alert on the rest. Un-tuned sensors are ignored within a month.
- **Encrypted traffic limits NIDS** to metadata (SNI, JA3/JA4, certificate, volume/timing) unless TLS is terminated for inspection.
- **Forward to [[SIEM]]** with context; a raw IDS console is not a detection programme.
- Test detections with replay/atomic tests; track coverage against [[MITRE ATT&CK]].

## Related

- [[Firewall]]
- [[WAF]]
- [[SIEM]]
- [[Endpoint Protection]]
- [[Threat Hunting]]
- [[Defences MOC]]
