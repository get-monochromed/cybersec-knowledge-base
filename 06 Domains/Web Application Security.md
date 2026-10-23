---
title: Web Application Security
aliases: [Web AppSec, Web Security]
category: domain
tags: [domain/web, appsec]
status: solid
up: "[[Domains MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Web Application Security

## Summary

Securing HTTP applications: browsers, APIs, and everything between. The dominant attack surface for most organisations, and the domain where the classic vulnerability classes ([[OWASP Top 10]]) are best documented.

## Threat model

- **Injection** — [[SQL Injection]], [[Cross-Site Scripting]], command injection, SSTI ([[Injection Attacks]]).
- **Authorization failures** — [[Broken Access Control]], IDOR, tenant isolation.
- **Authentication/session** — [[Session Hijacking]], credential stuffing, weak password reset flows.
- **Client-side** — [[Cross-Site Request Forgery]], XSS, clickjacking, postMessage abuse, prototype pollution.
- **Server-side** — SSRF (cloud metadata!), deserialisation, file upload, path traversal, XXE.
- **Supply chain** — vulnerable JS libraries, malicious npm packages ([[Supply Chain Attack]]).
- **Business logic** — price manipulation, race conditions, coupon abuse, workflow bypass.

## Controls

- **Secure SDLC**: [[Threat Modelling]] at design, SAST/DAST/SCA in CI, security tests per endpoint ([[Application Security]]).
- **Framework defaults**: output encoding, CSRF tokens, ORM parameterisation, secure cookies.
- **CSP + security headers**: `Content-Security-Policy`, HSTS, `X-Content-Type-Options`, `Referrer-Policy`, COOP/COEP.
- **WAF** as compensating control ([[WAF]]), rate limiting, bot management.
- **Secrets management**, least-privilege DB accounts, no verbose errors in production.
- **Logging**: auth events, authorization failures, admin actions ([[SIEM]]).

## Testing

- Manual testing with two accounts of different privilege finds the highest-impact bugs fastest.
- Automation finds the repeatable classes (injection, misconfig); humans find logic and authorization flaws.
- Bug bounty / pentest cadence for external surface ([[Penetration Testing]], [[Bug Bounty]]).

## Related

- [[OWASP Top 10]]
- [[Application Security]]
- [[Broken Access Control]]
- [[Injection Attacks]]
- [[Domains MOC]]
