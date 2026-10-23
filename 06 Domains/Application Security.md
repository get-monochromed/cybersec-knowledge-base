---
title: Application Security
aliases: [AppSec, Secure SDLC, SSDLC]
category: domain
tags: [domain/appsec, sdlc]
status: solid
up: "[[Domains MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Application Security

## Summary

Building security into how software is made, rather than testing it in at the end. Cheapest point to fix a defect is design; most expensive is production — which is why shift-left is an economic argument, not a slogan.

## Secure SDLC stages

1. **Requirements** — security requirements, abuse cases, compliance constraints ([[Threat Modelling]]).
2. **Design** — threat model, trust boundaries, authentication/authorization model, data classification.
3. **Implementation** — secure coding standards, approved libraries, secrets management, code review with a security lens.
4. **Verification** — SAST, SCA (dependencies), DAST, IaC scanning, fuzzing, [[Penetration Testing]] for critical paths.
5. **Release** — signed artifacts, SBOM, hardened build (SLSA), deployment gates.
6. **Operate** — runtime protection (RASP/WAF), monitoring, vulnerability response, incident feedback.

## Tooling

| Tool type | Finds | Weakness |
|---|---|---|
| SAST | code patterns, taint flows | false positives, misses runtime/config |
| SCA | vulnerable/malicious dependencies | noise, transitive depth |
| DAST | runtime vulnerabilities | shallow coverage, needs a running app |
| IAST | instrumented runtime | language/deployment constraints |
| Secrets scanning | committed credentials | needs pre-commit + history scan |
| IaC scanning | cloud misconfig in code | policy upkeep |

Feed all of it into one backlog with owners — five dashboards nobody triages is worse than one.

## Practices that actually reduce risk

- **Security champions** in each team, not a single gatekeeper.
- **Paved road**: secure defaults, templates, shared auth libraries — make the safe path the easy path.
- **Pre-commit hooks** for secrets/lint, so issues never reach review.
- **Dependency pinning and SBOM** ([[Supply Chain Attack]]).
- **Post-incident code review** — every incident produces a test or a lint rule.

## Related

- [[Web Application Security]]
- [[Threat Modelling]]
- [[Supply Chain Attack]]
- [[Container Security]]
- [[Domains MOC]]
