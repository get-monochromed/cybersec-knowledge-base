---
title: SIEM
aliases: [Security Information and Event Management, Log Management]
category: defensive
tags: [defensive/detection, platform]
status: solid
up: "[[Defensive Ops MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# SIEM

## Summary

Centralises logs, normalises them, correlates them and alerts on patterns. The SOC's memory and its primary detection platform — and, done badly, an expensive log dump nobody queries.

## Pipeline

1. **Collection** — agents (Windows Event Forwarding, syslog, Beats), APIs (cloud audit logs, SaaS, EDR), network devices, identity providers, applications.
2. **Parsing/normalisation** — into a common schema (ECS, OCSF, CIM).
3. **Enrichment** — asset criticality, identity context, threat intel, GeoIP.
4. **Storage** — hot/warm/cold tiers; retention driven by compliance and investigation needs ([[PCI DSS]] wants a year, 3 months readily available).
5. **Detection** — correlation rules, thresholds, anomaly/UEBA, Sigma rules.
6. **Alerting and case management** — into [[SOAR]] or a ticketing system.

## Essential log sources

Identity (AD/Entra/Okta), EDR, firewall/proxy, DNS, VPN, cloud control plane, email gateway, web servers, vulnerability scanner, backup infrastructure, and SaaS audit logs. Missing identity logs is the most common blind spot.

## Detection content

- **Sigma** — vendor-neutral rule format, converted to the platform's query language.
- Typical high-value rules: brute force then success, impossible travel, new inbox rule forwarding externally, LSASS access, shadow copy deletion, service creation after logon, mass file rename, EDR agent disabled, security group/IAM policy change.
- Tune relentlessly: every rule needs an owner, a test, and a false-positive review.

## Practical problems

- **Cost** — ingest-based pricing punishes verbose sources; filter at the edge, but not the security-relevant events.
- **Time skew** — no NTP = useless correlation.
- **Coverage theatre** — 1,000 rules, 990 unmaintained.
- **Data retention vs investigation** — attackers dwell for months; 30-day retention hides them.
- **Analyst usability** — if a query takes 10 minutes, nobody hunts.

## Alternatives/adjacent

Data lake + query engine (Elastic, Splunk, Sentinel, Snowflake + detection layer), XDR for endpoint-centric correlation, and [[SOAR]] for response. Many organisations run SIEM for compliance and XDR for actual detection.

## Related

- [[Security Operations Centre]]
- [[SOAR]]
- [[Threat Hunting]]
- [[Incident Response]]
- [[Defensive Ops MOC]]
