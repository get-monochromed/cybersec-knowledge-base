---
title: Denial of Service (DoS)
aliases: [DoS, DDoS, Distributed Denial of Service]
category: attack
tags: [attack/network, availability, exam]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Denial of Service (DoS)

## Summary

Making a service unavailable by exhausting a resource: bandwidth, connections, CPU, memory, disk, or the application's own logic. Availability attack, and the easiest one to mount at scale because the internet's protocols happily amplify traffic.

## Mechanism families

- **Volumetric** — flood the pipe: UDP floods, ICMP floods, DNS amplification. Measured in Gbps.
- **Protocol/state-exhaustion** — SYN flood, ACK flood, fragmented packets; exhaust connection tables.
- **Application layer (L7)** — HTTP floods, slowloris (hold connections open), expensive search queries, "one weird request" that triggers heavy backend work.
- **Reflection/amplification** — spoof the victim's IP and send to open DNS/NTP/memcached/CLDAP servers; a small request becomes a huge response (amplification factors up to 50,000× for memcached).
- **DoS by design** — a vulnerability that crashes the service (unhandled exception, ReDoS).
- **Resource exhaustion via business logic** — sign-up flood, expensive report generation, zip bomb.

## DDoS

Distributed version using a [[Botnet]] (Mirai-style IoT, or rented DDoS-for-hire). Modern extortion: "pay or we keep flooding". Also used as cover for another attack, or to distract the SOC.

## Detection

- Traffic anomalies: sudden protocol mix change, spike in half-open connections, many source IPs with identical payloads.
- Application metrics: latency up, error rate up, queue depth, CPU at 100% with low request diversity.
- CDN/WAF analytics usually detect before internal monitoring does.
- Note: if the attacker spoofs sources, log-based attribution is unreliable — resolve availability first.

## Mitigation

- **Upstream capacity**: CDN, anycast, scrubbing centres — you cannot out-provision a large DDoS on your own link.
- **SYN cookies**, connection limits, timeouts, rate limiting per IP/path/user.
- **WAF** for L7 patterns; autoscaling for elastic workloads.
- **Amplification hygiene**: block spoofed egress (BCP38), close open resolvers. You may be part of someone else's attack.
- **Reduce the blast radius**: static fallback page, graceful degradation, decouple dependencies.
- **Playbook**: who calls the ISP/CDN, thresholds to escalate, comms plan ([[Incident Response]]).

## Related

- [[Botnet]]
- [[Cyber Kill Chain]]
- [[Incident Response]]
- [[Firewall]]
- [[Attacks MOC]]
