---
title: Hardening
aliases: [System Hardening, Secure Configuration, Baseline]
category: defence
tags: [defence/operations, hygiene]
status: solid
up: "[[Defences MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Hardening

## Summary

Reducing the attack surface of a system by removing what is not needed and configuring what remains securely. Most breaches exploit a default, an unnecessary service, or a permissive setting — not a clever zero-day.

## Checklist by layer

**OS**
- Remove/disable unused services, protocols, shares, drivers, accounts.
- Disable SMBv1, LLMNR/NBT-NS, WDigest, legacy TLS; enable host firewall default-deny.
- Least-privilege accounts, LAPS for local admin, no shared admin passwords.
- Full-disk encryption, Secure Boot, screen lock, patching ([[Patch Management]]).

**Applications**
- Change defaults, disable sample apps and admin consoles, remove unused features.
- Least-privilege service accounts, secrets in a vault (not config files).
- Disable directory listing, verbose errors, unnecessary HTTP methods.

**Network devices**
- No management interface on the internet; MFA on admin; disable unused ports.
- Patch firmware (VPN/firewall CVEs are top initial access — see [[VPN]]).

**Cloud**
- No public buckets, IMDSv2, least-privilege IAM, no long-lived keys, logging on ([[Cloud Security]]).

**Containers**
- Minimal base images, non-root user, read-only rootfs, no privileged mode, dropped capabilities ([[Container Security]]).

## Benchmarks

Do not invent it: use **CIS Benchmarks** (per OS/product), vendor security guides, and **STIGs** where applicable. Automate with Ansible/Chef/Puppet, or image-baking so drift is impossible.

## Drift

Hardening decays: a new app requires a port, someone enables a service to debug. Controls:
- Configuration management with drift detection.
- CSPM for cloud, SCAP/OpenSCAP for hosts.
- Periodic re-baseline and exception register.

## Related

- [[Attack Surface]]
- [[Patch Management]]
- [[CIS Controls]]
- [[Operating System Security]]
- [[Defences MOC]]
