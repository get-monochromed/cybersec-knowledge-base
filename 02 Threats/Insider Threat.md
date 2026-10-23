---
title: Insider Threat
aliases: [Insider, Malicious Insider, Negligent Insider]
category: actor
tags: [actor/insider, identity]
status: solid
up: "[[Threats MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Insider Threat

## Summary

Threat originating from someone with legitimate access: employee, contractor, vendor, or a compromised account that behaves like one. Perimeter thinking fails here by definition — the insider is already inside, already authenticated, and usually already authorized for *something*.

## Three flavours

| Type | Intent | Detection difficulty | Primary control |
|---|---|---|---|
| **Malicious** | deliberate theft, sabotage, fraud | high (looks legitimate) | least privilege, separation of duties, monitoring |
| **Negligent** | none — falls for phishing, misconfigures, loses laptop | medium | [[Security Awareness Training]], fail-safe defaults, DLP |
| **Compromised** | attacker using valid credentials | very high | behavioural analytics, impossible travel, [[Zero Trust Architecture]] |

The compromised-insider case is why "insider threat" and "credential theft" overlap heavily — see [[Password Attacks]], [[Session Hijacking]], [[Phishing]].

## Red flags (behavioural + technical)

- Access patterns: bulk downloads, access outside role or hours, access to records not needed (the "curious nurse" pattern), printing/exporting at scale.
- Privilege accumulation, service accounts used interactively, shared credentials.
- HR context (notice period, grievance, financial stress) — handle with HR/legal, never by IT alone.
- Failed attempts followed by success, use of personal cloud storage, USB insertion, email forwarding rules, disabling logging.

## Controls

- **Least privilege + just-in-time access** ([[Security Principles]], [[Access Control Models]]) — limit what damage is even possible.
- **Separation of duties and dual control** for payments, key management, prod changes ([[Security Models|Clark-Wilson]]).
- **User behaviour analytics (UEBA)** in [[SIEM]]: baseline, then anomaly.
- **DLP** and egress monitoring; block personal storage and unauthorised SaaS.
- **Offboarding rigour**: revoke tokens, sessions, VPN, SaaS, shared passwords; recover hardware.
- **Culture**: report-friendly, no-blame for mistakes, so negligence surfaces early. Fear drives concealment.
- **Legal/HR**: monitoring must be lawful, disclosed, proportionate ([[GDPR]], [[DPDP Act 2023]]).

## Related

- [[Threat Actor]]
- [[Authentication, Authorization and Accounting]]
- [[Zero Trust Architecture]]
- [[Data Loss Prevention]]
- [[Threats MOC]]
