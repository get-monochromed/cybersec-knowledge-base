---
title: Broken Access Control
aliases: [IDOR, Insecure Direct Object Reference, Missing Function Level Access Control, BOLA]
category: attack
tags: [attack/web, owasp-a01, access-control, exam]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Broken Access Control

## Summary

The application lets a user do something they are not authorised to do — view another user's data, call an admin function, or modify a record they only have read access to. OWASP Top 10 #1, and the most common serious bug in real APIs. It is an authorization failure, not an authentication one.

## Root cause

[[Security Principles|Complete mediation]] is violated: the check exists at the UI or at one endpoint, but not on every request. Or the check is on the *identity* ("is logged in") rather than the *relationship* ("owns this record"). See [[Authentication, Authorization and Accounting]].

## Variants

- **IDOR / BOLA** — swapping an identifier: `/api/invoice/1001` → `1002`. Sequential IDs make it trivially detectable.
- **Forced browsing** — reaching `/admin` directly, bypassing a hidden menu.
- **Missing function-level control** — the API endpoint has no role check; only the frontend hides the button.
- **Horizontal** privilege escalation — same role, different user's data (the classic).
- **Vertical** privilege escalation — user → admin ([[Privilege Escalation]]).
- **Mass assignment** — posting `{"role":"admin"}` and the framework binds it (Rails `attr_accessible`, Spring `@ModelAttribute`).
- **JWT confusion** — trusting claims the client controls (e.g. `"role":"admin"` after a key confusion or missing signature check).
- **Path/directory traversal** — `../../etc/passwd` reaching files outside the intended root.
- **CORS misconfiguration** — `Access-Control-Allow-Origin: *` with credentials, or reflecting `Origin`, exposes authenticated APIs cross-site.
- **Missing tenant isolation** — multi-tenant SaaS returning another tenant's rows.

## Detection

- Test with **two accounts of different privilege** and replay every request with the other account's token — this finds most IDORs within an hour.
- Enumerate IDs; check whether 403s differ from 404s (leaks existence).
- SAST: endpoints without an authorization decorator/middleware; grep for `findById` without an ownership filter.
- Logs: many 403s or 404s from one session, sequential ID access, a user hitting admin routes.

## Mitigation

- **Deny by default** and authorize **server-side on every request**, using the record's ownership/relationship, not just the session.
- **Centralise authorization** — middleware, policy engine (OPA/Cedar), or framework guards — so it cannot be forgotten per-endpoint.
- **Use unguessable IDs** (UUIDv4/ULID) as defence in depth, never as the control.
- **Never trust client-supplied roles/tenant IDs**; derive them server-side from the session.
- **Framework mass-assignment protection** (allow-lists of writable fields).
- **Return 404 for unauthorized object access** where existence is sensitive.
- **Tests in CI** for every endpoint × every role; this is the only way it stays fixed.
- **[[OWASP Top 10]] A01**, [[CIS Controls]] 6 (access management).

## Related

- [[Authentication, Authorization and Accounting]]
- [[Access Control Models]]
- [[OWASP Top 10]]
- [[Privilege Escalation]]
- [[Attacks MOC]]
