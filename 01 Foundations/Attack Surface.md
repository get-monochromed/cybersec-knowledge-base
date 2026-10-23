---
title: Attack Surface
aliases: [Attack Surface Area, Exposure]
category: foundation
tags: [foundation/core, risk]
status: solid
up: "[[Foundations MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Attack Surface

## Summary

Every point where an attacker can interact with a system: ports, APIs, endpoints, user input fields, credentials, third-party dependencies, people, and physical access. Reduce it, measure it, and monitor it — you cannot defend what you have not enumerated.

## Components

- **Network surface** — exposed IPs, open ports, protocols, VPN endpoints, shadow IT, cloud storage buckets.
- **Application surface** — HTTP routes, parameters, file uploads, deserialisation, auth flows, mobile APIs, GraphQL introspection.
- **Human surface** — users who can be phished, admins who can be social-engineered ([[Social Engineering]]).
- **Supply chain surface** — dependencies, CI/CD pipelines, third-party SaaS, managed service providers ([[Supply Chain Attack]]).
- **Data surface** — credentials in code, secrets in CI, backups, logs containing PII.
- **Physical surface** — removable media, unlocked racks, printers, USB ports.

## Attack surface vs attack vector

The *surface* is the set of reachable interfaces. A *vector* is a specific path used to exploit one (email attachment, exposed RDP, watering hole). See [[Attack Taxonomy]].

## Management

1. **Discover** — asset inventory, external attack surface management (EASM), cloud posture scanning, subdomain enumeration (see [[Reconnaissance]] — attackers do exactly this).
2. **Classify** — internet-facing vs internal, data sensitivity, business criticality.
3. **Reduce** — close unused ports and services, remove old endpoints, decommission unused accounts, delete stale DNS records (subdomain takeover).
4. **Detect** — monitor for new exposures; new exposure appears with every deploy.
5. **Prioritise** — see [[Risk Management]]; a low-severity bug on an internet-facing auth endpoint outranks a critical bug on an isolated lab box.

## Metrics

Attack surface size is a leading indicator: exposed services per host, public endpoints count, third-party integrations, number of privileged accounts. Shrinking it reduces the probability that *any* vulnerability is reachable.

## Related

- [[Security Principles]]
- [[Defence in Depth]]
- [[Reconnaissance]]
- [[Vulnerability Management]]
- [[Zero Trust Architecture]]
- [[Foundations MOC]]
