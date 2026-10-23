---
title: Nation-State Actor
aliases: [State-Sponsored, State Actor, APT (state)]
category: actor
tags: [actor/state]
status: developing
up: "[[Threats MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Nation-State Actor

## Summary

An actor operating with state resources, direction or tolerance. Distinct from [[Advanced Persistent Threat]] in that this describes the *sponsor*; an APT describes the *behaviour*. Practically the two overlap almost completely.

## Motivation

Espionage (political, military, economic), intellectual property theft, pre-positioning for conflict, disruption of critical infrastructure, influence operations, currency generation to fund operations.

## Capability

The top of the capability ladder:

- Custom malware, bootkits, firmware implants.
- Zero-day exploitation (zero-days) and long-held vulnerabilities.
- Supply-chain compromise (build systems, managed service providers, network devices).
- Deep infrastructure: false flags, compromised third-party networks as jumping hosts.
- Patience and legal impunity.

## Typical targets

Government and defence, critical infrastructure ([[OT and ICS Security]]), telecoms, energy, research universities, diaspora and journalists, and the *suppliers* of all of the above.

## Typical TTPs

- Credential-based access, phishing with high-quality lures, edge appliance exploitation.
- [[Living off the Land]] and abuse of cloud identity (token theft, consent phishing).
- Long-dwell quiet collection, exfiltration via legitimate cloud services.
- Wiper malware and destructive attacks in wartime or as coercion.

## Defensive reality

- Deterrence is largely diplomatic/legal; defence is technical and intelligence-led.
- Prioritise: identity hardening, egress monitoring, segmentation of critical systems, supply-chain assurance, log retention long enough to investigate (months, not days).
- Attribution is slow and often uncertain; do not let attribution delay containment ([[Incident Response]]).

## Related

- [[Advanced Persistent Threat]]
- [[Threat Intelligence]]
- [[Supply Chain Attack]]
- [[OT and ICS Security]]
- [[Threats MOC]]
