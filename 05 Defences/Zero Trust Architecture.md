---
title: Zero Trust Architecture
aliases: [Zero Trust, ZTNA, BeyondCorp]
category: defence
tags: [defence/architecture, identity]
status: solid
up: "[[Defences MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: ["NIST SP 800-207"]
---

# Zero Trust Architecture

## Summary

"Never trust, always verify." No implicit trust based on network location — every request is authenticated, authorized and encrypted based on identity, device posture and context. It is an architecture philosophy, not a product.

## Principles (NIST 800-207)

1. All data sources and services are resources; the network is not the security boundary.
2. All communication is secured regardless of location.
3. Access is granted per-session, on a per-request basis.
4. Access is determined by dynamic policy: identity, device, behaviour, sensitivity.
5. Continuous monitoring and posture assessment; re-evaluate continuously.
6. Least privilege applies to both users and workloads.
7. Assume breach — design for containment and telemetry.

## Building blocks

- **Identity provider / SSO** + strong MFA (FIDO2) — the new perimeter ([[Authentication, Authorization and Accounting]]).
- **Policy engine + policy enforcement point** — per-app proxy/gateway.
- **Device posture** — managed, patched, encrypted, compliant.
- **Microsegmentation** — workload-to-workload, not just user-to-app ([[Network Segmentation]]).
- **Continuous verification** — risk signals (impossible travel, unmanaged device, malware) trigger step-up auth or deny (CAE/Conditional Access).
- **Telemetry everywhere** — you cannot verify what you cannot see ([[SIEM]]).

## Migration path (pragmatic)

1. Inventory apps and data flows; classify.
2. Put SSO + MFA in front of everything; kill local accounts and shared passwords.
3. Replace VPN with **ZTNA** for third parties and remote staff, app by app.
4. Segment the crown jewels; enforce identity-aware policy between zones.
5. Add device posture and continuous evaluation; retire static network trust.
6. Extend to workloads (service identity, mTLS, workload attestation).

## Common misconceptions

- "Zero trust means no firewall" — no, it means policy on identity and context rather than IP.
- "Buy a ZTNA appliance and you are done" — without identity hygiene and inventory it just relocates the problem.
- "It is a project" — it is continuous, and it fails if users route around it (make the compliant path the easiest path).

## Related

- [[Network Segmentation]]
- [[VPN]]
- [[Security Principles]]
- [[Access Control Models]]
- [[NIST CSF]]
- [[Defences MOC]]
