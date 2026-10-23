---
title: Authentication, Authorization and Accounting
aliases: [AAA, Triple A, AuthN AuthZ]
category: foundation
tags: [foundation/core, identity, exam]
status: solid
up: "[[Foundations MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Authentication, Authorization and Accounting (AAA)

## Summary

The identity pipeline: prove who you are (authentication), decide what you may do (authorization), record what you did (accounting). In that order — every "broken access control" incident is one of these three being skipped or conflated.

## Authentication (AuthN) — who are you

Proven via factors:

- **Something you know** — password, PIN, security question
- **Something you have** — TOTP app, hardware token (FIDO2/WebAuthn), smart card
- **Something you are** — fingerprint, face, iris
- **Somewhere you are / something you do** — geolocation, behavioural biometrics (weaker, contextual)

**MFA** requires two *different* categories; two passwords is not MFA. **Passwordless** replaces the password with a possession factor plus biometric unlock.

Protocols and mechanisms: passwords (hashed with bcrypt/Argon2 — see [[Hashing]]), [[TLS]] client certificates, [[Digital Signatures and PKI|PKI]], Kerberos, OAuth 2.0 / OIDC (delegated auth), SAML (enterprise SSO), RADIUS/TACACS+ (network devices).

Failure modes: [[Password Attacks]], [[Phishing]] (including MFA fatigue/push bombing), session token theft ([[Session Hijacking]]).

## Authorization (AuthZ) — what may you do

Decided *after* authentication, on every request. Models: [[Access Control Models]] (DAC, MAC, RBAC, ABAC, ReBAC). Implemented as ACLs, capability tokens, policy engines (OPA), cloud IAM policies. OWASP's #1 web risk is [[Broken Access Control]].

Golden rule: **authenticate at the front door, authorize at every door.** Hiding a button is not authorization.

## Accounting / Auditing — what did you do

Logging of identity, action, object, result, timestamp, source. Feeds [[SIEM]], [[Digital Forensics]], compliance ([[PCI DSS]], [[ISO 27001]] A.8.15) and non-repudiation.

Requirements: trustworthy time source, tamper-resistant storage (append-only/WORM), retention policy, PII minimisation, and alerting on gaps. An account that logs in but generates no audit trail is a red flag.

## Where it shows up

- **Zero Trust** = authenticate and authorize every request, not just at the perimeter ([[Zero Trust Architecture]]).
- **Privileged access** = separate, stronger AAA for admins (PAM, just-in-time access, break-glass accounts).
- **Incident response** = accounting is the difference between "something happened" and "here is exactly what happened".

## Related

- [[CIA Triad]]
- [[Access Control Models]]
- [[Password Attacks]]
- [[Session Hijacking]]
- [[Zero Trust Architecture]]
- [[Foundations MOC]]
