---
title: Cloud Security
aliases: [Cloud Security Domain, CSPM, Cloud Native Security]
category: domain
tags: [domain/cloud, iam]
status: solid
up: "[[Domains MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Cloud Security

## Summary

Security of cloud-hosted workloads and services. The technical controls change shape but the failures are familiar: identity misuse, misconfiguration, and no visibility. The attacker's favourite target is the control plane (IAM), not the hypervisor.

## Shared responsibility

The provider secures the cloud *of* cloud (hardware, hypervisor, managed service internals); you secure what is *in* it (configuration, identity, data, workloads). The line moves per service: for IaaS you patch the OS; for SaaS you mostly manage identity and data sharing. Most "cloud breaches" are customer-side misconfiguration.

## Core risks

- **Identity** — over-privileged roles, long-lived access keys, `*:*` policies, role chaining to admin, missing MFA on root.
- **Public exposure** — storage buckets, databases, snapshots, management consoles on 0.0.0.0/0.
- **Metadata service abuse** — SSRF → `169.254.169.254` → instance credentials ([[Injection Attacks|SSRF]]).
- **Secrets in code/images/CI** — keys in repos, environment variables in build logs.
- **Logging gaps** — CloudTrail/Activity Log disabled, no central retention.
- **Multi-tenancy** — isolation bugs, cross-account role trust misconfiguration.
- **Serverless** — over-privileged function roles, event injection, dependency risk.
- **Kubernetes** — see [[Container Security]].

## Controls

- **Identity first**: SSO + MFA, no root use, short-lived credentials (OIDC federation from CI), permission boundaries, access analysers.
- **Guardrails as code**: IaC scanning, SCPs/org policies that hard-block public buckets and unapproved regions.
- **CSPM** (configuration posture) + **CWPP** (workload) + **CIEM** (entitlements) — or the equivalent native tools; alert, do not just report.
- **Network**: VPC segmentation, private endpoints, egress control, no public admin ports (use bastion/SSM).
- **Data**: encryption with customer-managed keys, bucket policies, object lock for backups.
- **Detection**: centralise control-plane logs to the [[SIEM]]; alert on IAM changes, key creation, logging disabled, security-group opens.

## Related

- [[Container Security]]
- [[Zero Trust Architecture]]
- [[Backup and Recovery]]
- [[Data Loss Prevention]]
- [[Domains MOC]]
