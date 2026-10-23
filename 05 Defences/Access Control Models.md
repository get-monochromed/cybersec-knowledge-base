---
title: Access Control Models
aliases: [DAC, MAC, RBAC, ABAC, ReBAC, Access Control]
category: defence
tags: [defence/identity, access-control, exam]
status: solid
up: "[[Defences MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Access Control Models

## Summary

How a system decides whether a subject may perform an action on an object. This is *authorization* in practice — the part of [[Authentication, Authorization and Accounting|AAA]] where most serious vulnerabilities live.

## The models

| Model | Decision based on | Example | Strength / weakness |
|---|---|---|---|
| **DAC** (discretionary) | owner's discretion, ACLs | file permissions, SharePoint sharing | flexible; users over-share |
| **MAC** (mandatory) | system-assigned labels + clearance | SELinux, military classification | strong containment; rigid |
| **RBAC** (role-based) | job role → permissions | enterprise apps, AWS roles | manageable at scale; role explosion |
| **ABAC** (attribute-based) | attributes: user, resource, environment | "managers can approve ≤ ₹1L during business hours in India" | expressive, context-aware; complex to audit |
| **ReBAC** (relationship-based) | graph of relationships | Google Zanzibar, "owner of the doc's parent folder" | perfect for collaboration apps; needs a graph engine |
| **Rule-based** | explicit rules/policies | firewall rules, conditional access | simple; hard to reason about in aggregate |

Formal underpinnings: [[Security Models]] (Bell-LaPadula for MAC confidentiality, Biba for integrity, Clark-Wilson for transactions).

## Implementation building blocks

- **ACLs** — per-object lists of subject→permissions (NTFS, POSIX).
- **Capabilities / tokens** — possession grants access (Kerberos tickets, OAuth scopes, JWT claims).
- **Policy engines** — centralised decisions: OPA/Rego, Cedar, AWS IAM policies, Azure RBAC.
- **Groups and nesting** — convenient, but creates transitive privilege; always compute effective permissions.
- **Just-in-time elevation** — time-bound, approved privilege (PAM, `sudo` with approval).

## Design rules

1. **Deny by default**, allow explicitly.
2. **Least privilege**, with review and expiry — permissions accumulate otherwise ("privilege creep").
3. **Check on every request** server-side, using the object relationship, not just the session ([[Broken Access Control]]).
4. **Separation of duties** for sensitive operations ([[Security Principles]]).
5. **Model the org, then the app** — role explosion is usually a sign of mapping roles to individuals rather than jobs.
6. **Recertify** access periodically; stale accounts are both an audit finding and an attack path ([[Insider Threat]]).

## Where it goes wrong

- Effective permissions nobody can compute (nested groups, wildcards, `*:*`).
- Client-side enforcement (hidden buttons).
- Role checks that ignore the tenant/owner dimension.
- Orphaned admin accounts and service accounts with static keys.

## Related

- [[Authentication, Authorization and Accounting]]
- [[Security Models]]
- [[Zero Trust Architecture]]
- [[Broken Access Control]]
- [[Defences MOC]]
