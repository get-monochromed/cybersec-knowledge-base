---
title: Security Models
aliases: [Access Control Models (formal), Bell-LaPadula, Biba, Clark-Wilson]
category: foundation
tags: [foundation/core, access-control, exam]
status: developing
up: "[[Foundations MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Security Models

## Summary

Formal descriptions of how a system enforces confidentiality or integrity. They come up constantly in exams and interviews even though real systems implement looser versions. Know the two rules each is famous for.

## Confidentiality models

**Bell-LaPadula** — military multilevel security, "no read up, no write down":

- *Simple security property*: a subject cannot read an object of higher classification.
- *\*-property (star)*: a subject cannot write to an object of lower classification (prevents leaking secrets downward).
- *Discretionary* property: access per ACL.
- Weakness: no integrity protection — the focus is on secrecy, so a low-integrity high-classification document is allowed.

**Brewer-Nash (Chinese Wall)** — dynamically prevents conflicts of interest: once you access one client's data in a conflict class, you cannot access a competitor's. Classic for consultancies, banks, audit firms.

## Integrity models

**Biba** — the mirror image of Bell-LaPadula, "no read down, no write up":

- *Simple integrity*: no read of lower integrity objects (can't trust dirty data).
- *\*-integrity*: no write to higher integrity objects (can't contaminate trusted data).
- *Invocation* property: subjects can't invoke higher-integrity subjects.

**Clark-Wilson** — commercial integrity: users act on data only through *well-formed transactions* (programs), with separation of duties between certifier and approver, and logged (audited) state transitions. This maps closely to real business apps and to [[Security Principles|separation of duties]].

## Access control families (implementation-facing)

See [[Access Control Models]] for DAC, MAC, RBAC, ABAC, ReBAC.

| Model | Type | One-line |
|---|---|---|
| Harrison-Ruzzo-Ullman | formal | access matrix with decidable safety checks |
| Graham-Denning | formal | 8 primitive operations to securely create/delete subjects and objects |
| Take-Grant | graph | rights propagation via take/grant edges |
| Lattice | structure | mandatory levels forming a partial order |

## Why they matter in practice

- MAC-style ideas → SELinux/AppArmor, Windows integrity levels, classification labels in [[Cloud Security]].
- RBAC → the default for enterprise apps.
- Biba/Clark-Wilson thinking → why financial systems require dual control and immutable ledgers.
- All of them → vocabulary for arguing in an audit that a design is deliberate.

## Related

- [[Access Control Models]]
- [[Security Principles]]
- [[CIA Triad]]
- [[Authentication, Authorization and Accounting]]
- [[Foundations MOC]]
