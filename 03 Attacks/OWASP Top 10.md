---
title: OWASP Top 10
aliases: [OWASP Top Ten, OWASP]
category: attack
tags: [attack/web, owasp, framework, exam]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-24
sources: ["https://owasp.org/Top10/", "https://top10.owasp.org/2025/ (list order, ingested 2026-10-24)"]
---

# OWASP Top 10

## Summary

The best-known awareness document for web application security: ten risk categories ranked from real-world data. It is a *starting point for awareness*, not a checklist or a standard, and not exhaustive.

## 2025 list (current)

| # | Category | Core issue | Note |
|---|---|---|---|
| A01 | [[Broken Access Control]] | missing or incorrect authorization | still the most common serious finding |
| A02 | Security Misconfiguration | defaults, exposed services, verbose errors, unnecessary features | up from #5 — see [[Hardening]] |
| A03 | Software Supply Chain Failures | dependencies, build pipeline, update channels | new/expanded category — see [[Supply Chain Attack]] |
| A04 | Cryptographic Failures | weak or missing crypto, plaintext storage | see [[Cryptography]] |
| A05 | [[Injection Attacks]] | SQLi, XSS, command, template injection | dropped from #3; parameterise, encode |
| A06 | Insecure Design | missing threat modelling and abuse cases | see [[Threat Modelling]] |
| A07 | Authentication Failures | weak auth, credential stuffing, session handling | see [[Authentication, Authorization and Accounting]] |
| A08 | Software or Data Integrity Failures | unsigned updates, insecure deserialisation, unverified data | see [[Digital Signatures and PKI]] |
| A09 | Security Logging and Alerting Failures | no detection, no alerting, no response | see [[SIEM]] |
| A10 | Mishandling of Exceptional Conditions | error, edge-case and failure paths handled unsafely | no dedicated note yet — see glossary |

### What moved from 2021

| Change | Detail |
|---|---|
| **A02 Security Misconfiguration** | #5 → #2. Configuration, not code, is increasingly the exposure |
| **A03 Software Supply Chain Failures** | new at #3, and broader than the old "Vulnerable and Outdated Components". Dependency, build-pipeline and updater compromise are now one category |
| **A05 Injection** | #3 → #5; still present, no longer the headline |
| **A07** | renamed from "Identification and Authentication Failures" to "Authentication Failures" |
| **A09** | renamed from "Security Logging and Monitoring" to "Security Logging and Alerting" — emphasis on the alert, not the log |
| **A10** | "Mishandling of Exceptional Conditions" replaces Server-Side Request Forgery |
| **SSRF** | no longer its own category; absorbed into A01 (see the warning below) |
| **Vulnerable and Outdated Components** | no longer a standalone category; subsumed by A03 |

Tag numbering across the vault now follows the 2025 list: `owasp-a03` means supply chain, `owasp-a05` means injection. Older notes using 2021 tags were renumbered during the 2026-10-24 ingest.

> [!warning] Unverified — where SSRF went, and what the categories contain
> The ingested source was a list of ten titles with links only — no definitions, no data, no mapping notes. The titles and their order are authoritative; the "core issue" descriptions are the vault's own wording, and the claim that SSRF was **absorbed into A01** is an inference from its absence, not something OWASP is quoted as saying. Read `top10.owasp.org/2025` for the actual definitions before citing them. Likewise A10's scope is unknown here beyond its name — treat it as "a category exists" rather than knowledge.

## 2021 list (superseded)

Retained for historical reference and for reading older reports. Do not use for new mappings.

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

## How to actually use it

- Map findings to categories for reporting and trend analysis.
- Use A06 (insecure design) to justify [[Threat Modelling]] before code.
- Use A03 (supply chain) to justify an SBOM and dependency pinning — the 2025 list promotes it to a top-three risk ([[Supply Chain Attack]]).
- Use A10 as a review prompt: what happens on timeout, partial failure, malformed input, missing environment variable, or a rejected authorisation check? Fail-open error handling is an access-control bug wearing a different hat ([[Security Principles]]).
- Do **not** treat "we cover the Top 10" as a security programme: it omits business logic abuse, API-specific risks (see OWASP API Security Top 10), and infrastructure.
- Pair with [[CIS Controls]] (operational hygiene) and [[NIST CSF]] (programme structure).

## Related

- [[Web Application Security]]
- [[Broken Access Control]]
- [[Injection Attacks]]
- [[Application Security]]
- [[Supply Chain Attack]]
- [[Attacks MOC]]
