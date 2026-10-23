---
title: Hacktivist
aliases: [Hacktivism, Ideological Attacker, Anonymous]
category: actor
tags: [actor/ideological]
status: solid
up: "[[Threats MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Hacktivist

## Summary

Ideologically motivated actor seeking publicity, disruption or political change. Success is measured in attention, so targets are chosen for symbolic value — and defacement or DDoS makes a better headline than quiet data theft.

## Motivation

Political, social, environmental, religious, or protest against a specific organisation. Reputation inside a group matters.

## Capability

Wide range: from low-skill participants in a collective (Anonymous-style) to technically strong groups. Common pattern is a small core with a large, disposable crowd for DDoS and scanning.

## Typical TTPs

- [[Denial of Service (DoS)]] — the signature move: volumetric, application-layer, and "hydra" DDoS tools.
- Website defacement, doxxing, leaking internal documents.
- [[SQL Injection]] and credential reuse against poorly maintained targets.
- Social media and [[Social Engineering]] for recruitment and intelligence.
- Data theft with public release (leaks) rather than extortion.

## Defensive focus

- Availability engineering: DDoS protection, CDN, autoscaling, rate limiting.
- [[Web Application Security]] and patch hygiene for public sites.
- Brand/reputation monitoring and a prepared [[Incident Response]] comms plan — the public narrative is part of the incident.
- Watch for insider sympathy (overlaps [[Insider Threat]]).

## Related

- [[Cybercriminal]]
- [[Denial of Service (DoS)]]
- [[Threat Actor]]
- [[Incident Response]]
- [[Threats MOC]]
