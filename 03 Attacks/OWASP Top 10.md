---
title: OWASP Top 10
aliases: [OWASP Top Ten, OWASP]
category: attack
tags: [attack/web, owasp, framework, exam]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: ["https://owasp.org/Top10/"]
---

# OWASP Top 10

## Summary

The best-known awareness document for web application security: ten risk categories ranked from real-world data. It is a *starting point for awareness*, not a checklist or a standard, and not exhaustive.

## 2021 list

| # | Category | Core issue | Note |
|---|---|---|---|
| A01 | [[Broken Access Control]] | missing/incorrect authorization | most common serious finding |
| A02 | Cryptographic Failures | weak/missing crypto, plaintext storage | see [[Cryptography]] |
| A03 | [[Injection Attacks]] | SQLi, XSS, command, template injection | parameterise, encode |
| A04 | Insecure Design | missing threat modelling and abuse cases | see [[Threat Modelling]] |
| A05 | Security Misconfiguration | defaults, open buckets, verbose errors, unnecessary features | see [[Hardening]] |
| A06 | Vulnerable and Outdated Components | unpatched libraries, EOL software | see [[Vulnerability Management]] |
| A07 | Identification and Authentication Failures | weak auth, credential stuffing, session issues | see [[Authentication, Authorization and Accounting]] |
| A08 | Software and Data Integrity Failures | insecure deserialisation, unsigned updates/CI | see [[Supply Chain Attack]] |
| A09 | Security Logging and Monitoring Failures | no detection, no response | see [[SIEM]] |
| A10 | Server-Side Request Forgery (SSRF) | server fetches attacker-chosen URL | cloud metadata theft |

> [!warning] Unverified — 2025 revision
> A 2025 edition has been in release-candidate circulation and reportedly reshuffles categories (supply chain elevated, security misconfiguration moved up, "mishandling of exceptional conditions" added). The details here are not verified against the final document — check owasp.org/Top10 and correct this table.

## How to actually use it

- Map findings to categories for reporting and trend analysis.
- Use A04 (insecure design) to justify [[Threat Modelling]] before code.
- Do **not** treat "we cover the Top 10" as a security programme: it omits business logic abuse, API-specific risks (see OWASP API Security Top 10), and infrastructure.
- Pair with [[CIS Controls]] (operational hygiene) and [[NIST CSF]] (programme structure).

## Related

- [[Web Application Security]]
- [[Broken Access Control]]
- [[Injection Attacks]]
- [[Application Security]]
- [[Attacks MOC]]
