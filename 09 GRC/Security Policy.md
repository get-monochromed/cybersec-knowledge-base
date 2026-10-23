---
title: Security Policy
aliases: [Policy, Information Security Policy, ISP, Policy Hierarchy]
category: grc
tags: [grc/governance, policy]
status: solid
up: "[[GRC MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Security Policy

## Summary

Written management intent. Policies are how an organisation turns risk decisions into enforceable expectations — and how it proves, to an auditor or a court, that expectations existed.

## Hierarchy

| Level | Answers | Example | Changes how often |
|---|---|---|---|
| **Policy** | what and why (mandatory) | "Access is granted on least privilege" | yearly, by management |
| **Standard** | specific requirements | "Passwords ≥ 16 chars, MFA for admin" | as technology changes |
| **Procedure** | step-by-step how | "Joiner/mover/leaver process" | often |
| **Guideline** | recommended practice | "How to choose a password manager" | freely |

Everything should trace upward: a control exists because a policy requires it, and an exception is a time-limited deviation from a standard.

## Minimum policy set

Acceptable use · access control · asset management · password/authentication · remote access · data classification · encryption · backup · incident response · business continuity · vulnerability/patch management · secure development · supplier security · privacy · acceptable AI use.

## What makes a policy useful

- **Enforceable and enforced** — an unenforced policy is worse than none (it creates liability without protection).
- **Readable** — two pages, not forty. Long policies are acknowledged and ignored.
- **Owned** — a named owner and a review date.
- **Exception process** — with risk acceptance, approval, and expiry ([[Risk Management]]).
- **Accessible** — an intranet page nobody finds does not exist.
- **Aligned to a framework** so audit evidence is a by-product ([[ISO 27001]], [[CIS Controls]]).

## Related

- [[ISO 27001]]
- [[Compliance Audit]]
- [[Security Awareness Training]]
- [[Risk Management]]
- [[GRC MOC]]
