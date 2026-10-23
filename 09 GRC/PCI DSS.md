---
title: PCI DSS
aliases: [Payment Card Industry Data Security Standard, PCI]
category: grc
tags: [grc/standard, payments, exam]
status: solid
up: "[[GRC MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: ["PCI DSS v4.0.1"]
---

# PCI DSS

## Summary

A contractual standard for anyone storing, processing or transmitting cardholder data. Enforced by the card brands through acquirers — so non-compliance is a commercial problem, not just a legal one.

## The 12 requirements (v4.0)

1. Install and maintain network security controls (firewalls)
2. Apply secure configurations (no vendor defaults)
3. Protect stored account data (minimise, encrypt, key management)
4. Protect cardholder data in transit with strong cryptography
5. Protect all systems against malware; update AV/anti-malware
6. Develop and maintain secure systems and software
7. Restrict access by business need to know
8. Identify and authenticate access (MFA for all access into the CDE, unique IDs)
9. Restrict physical access to cardholder data
10. Log and monitor all access (retain 12 months, 3 months immediately available)
11. Test security regularly (ASV scans quarterly, internal/external pentests annually)
12. Support information security with policies and programmes (training, IR plan, risk assessment)

## Scope

The **Cardholder Data Environment (CDE)** — systems that store, process, or transmit card data, plus connected systems. Scope reduction is the primary cost lever: **tokenisation**, network segmentation, and not storing data at all.

## Validation

- **SAQ** (self-assessment) for smaller merchants depending on channel and volume.
- **ROC** by a **QSA** for larger merchants/service providers.
- **ASV** (Approved Scanning Vendor) quarterly external scans.
- **Attestation of Compliance (AoC)** is what acquirers actually ask for.

## v4.0 direction (future-dated requirements)

Themes: **targeted risk analyses** for each requirement, expanded **MFA** to all CDE access, **e-commerce** requirements (scripts on payment pages — 6.4.3/11.6.1), **authenticated internal vulnerability scans**, and a documented **cryptographic inventory**.

## Practical reality

- Compliance ≠ security, but PCI does force useful basics: segmentation, logging, MFA, patching.
- The hardest parts in practice: scoping correctly, logging sufficiently, and maintaining evidence throughout the year rather than the week before the audit.

## Related

- [[Compliance Audit]]
- [[Network Segmentation]]
- [[ISO 27001]]
- [[GRC MOC]]
