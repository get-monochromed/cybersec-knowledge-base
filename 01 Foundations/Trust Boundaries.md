---
title: Trust Boundaries
aliases: [Trust Boundary]
category: foundation
tags: [foundation/core, design, threat-modelling]
status: developing
up: "[[Foundations MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Trust Boundaries

## Summary

A trust boundary is any line where data or control passes between components with different privilege or trust levels. Every serious vulnerability lives on one, because that is where validation and authorization are either done or forgotten.

## Where they are

- Browser ↔ web server (all user input)
- Web app ↔ database (queries, stored procedures)
- Application ↔ OS (command execution, file paths)
- Container ↔ host / container ↔ container
- Corporate network ↔ internet, and increasingly user ↔ internal app (see [[Zero Trust Architecture]])
- Tenant ↔ tenant in SaaS (the worst kind of bug: cross-tenant data leak)
- User process ↔ privileged process (setuid binaries, Windows services, sudo)
- CI/CD ↔ production (deployment credentials)

## Why they matter

Within a boundary, code often trusts its inputs. Across one, it must not. [[Threat Modelling]] starts by drawing them; STRIDE is applied per boundary crossing. Classic boundary failures:

- Missing authorization check on an internal API assumed to be "internal only" → [[Broken Access Control]].
- Input passed to a shell → [[Injection Attacks]].
- Path built from user input → directory traversal.
- Trusting a `X-Forwarded-For` header for authorization.
- Implicit trust of anything inside the VPN → the reason lateral movement is so effective ([[Lateral Movement]]).

## Rules of thumb

- Validate on the *receiving* side of the boundary, always.
- Authenticate and authorize at every crossing, not once per session.
- Data crossing outward should be minimised and sanitised (avoid leaking stack traces, versions, internal hostnames).
- Draw the diagram first; the bugs are usually on the arrows that nobody drew.

## Related

- [[Threat Modelling]]
- [[Attack Surface]]
- [[Security Principles]]
- [[Broken Access Control]]
- [[Zero Trust Architecture]]
- [[Foundations MOC]]
