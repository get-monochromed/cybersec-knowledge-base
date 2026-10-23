---
title: Security Principles
aliases: [Security Design Principles, Saltzer and Schroeder]
category: foundation
tags: [foundation/core, design, exam]
status: solid
up: "[[Foundations MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Security Principles

## Summary

Design rules that keep showing up in every standard. Saltzer & Schroeder (1975) is still the canonical list; NIST SP 800-160 and every secure-coding guide restate it.

## The list

- **Least privilege** — give the minimum access needed, for the minimum time. Root-by-default, wildcard IAM policies and `sudo ALL` all violate it. Enforced with [[Access Control Models]], PAM, just-in-time access.
- **Separation of duties** — no single person can complete a sensitive action alone (requester ≠ approver). Prevents fraud and limits insider damage ([[Insider Threat]]).
- **Defence in depth** — layers, so one bypass is not game over. See [[Defence in Depth]].
- **Fail securely (fail-safe defaults)** — on error, deny. A crashed auth check must not return "allowed". Default-deny firewalls and allow-lists.
- **Economy of mechanism** — simple, small, auditable designs. Complexity is where bugs hide.
- **Complete mediation** — check authorization on *every* access, not once at login (see [[Broken Access Control]]).
- **Open design** — security must not depend on the secrecy of the design (Kerckhoffs's principle, see [[Cryptography]]); only keys are secret.
- **Least common mechanism** — avoid shared state between users (shared temp dirs, shared caches) where it enables leakage.
- **Psychological acceptability** — if it is unusable, people bypass it (sticky notes, shared passwords, disabled MFA).
- **Minimise attack surface** — every open port, feature and account is a liability ([[Attack Surface]]).
- **Secure by default** — the safe configuration must be the default one.
- **Zero trust / verify explicitly** — trust nothing implicitly, including the internal network ([[Zero Trust Architecture]]).

## How to use it

Two applications:

1. **Review existing systems** — walk each principle and ask "where is this violated?" It finds real issues fast (usually least privilege and complete mediation).
2. **Design review** — when proposing a control, name the principle it implements. "We added rate limiting" → economy of mechanism + availability.

## Common violations seen in the wild

| Violation | Real-world shape |
|---|---|
| Least privilege | Service accounts with domain admin |
| Complete mediation | API trusts a client-supplied `role` field |
| Fail-safe defaults | `except: return True` in an authz check |
| Separation of duties | One admin can both deploy and approve the deploy |
| Minimise attack surface | 40 unused services on an internet-facing host |

## Related

- [[CIA Triad]]
- [[Defence in Depth]]
- [[Attack Surface]]
- [[Access Control Models]]
- [[Security Controls]]
- [[Zero Trust Architecture]]
- [[Foundations MOC]]
