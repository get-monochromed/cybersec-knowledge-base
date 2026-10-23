---
title: WAF
aliases: [Web Application Firewall]
category: defence
tags: [defence/web, detection]
status: solid
up: "[[Defences MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# WAF

## Summary

An HTTP-aware reverse proxy that inspects requests/responses and blocks attacks against a web application — [[SQL Injection]], [[Cross-Site Scripting]], known CVE patterns, bots, and rate abuse. Useful, but a compensating control: it does not fix the vulnerability.

## Deployment modes

- **Reverse proxy / inline** (cloud WAF, ModSecurity+CRS, AWS WAF) — blocks or challenges.
- **Out-of-band** — monitors only, no blocking (safe for tuning).
- **Integrated** in a CDN/edge (Cloudflare, Akamai) — also gives DDoS absorption.
- **RASP / in-app** — instrumentation inside the runtime, sees post-decoding data.

## Detection techniques

- **Negative security model** — signatures/regex for attack patterns (CRS rules). Good default, evadable with encoding.
- **Positive security model** — allow-list valid parameter shapes; high effort, strong.
- **Behavioural/bot** — rate, sequence, fingerprint, challenge.
- **Virtual patching** — vendor rules for a CVE you cannot yet patch; buy time, not a substitute for the patch.

## Limits

- Evasion via encoding, JSON/XML nesting, chunked bodies, HTTP/2 quirks, parameter pollution.
- Business-logic abuse (e.g. [[Broken Access Control]] IDOR) looks like normal traffic — a WAF cannot tell that `id=1002` is not yours.
- TLS termination needs care; API traffic without standard HTTP patterns bypasses classic rules.
- Tuning debt: blocklists that break legitimate traffic get disabled.

## Operating it

- Start in monitor mode, tune, then block. Track false positives per rule.
- Alert on rule hits into the [[SIEM]] — hit volume is a good "someone is poking us" signal.
- Keep the rule set updated; log full request context for [[Incident Response]].
- Measure what it actually blocked vs. what got through — test with the [[Offensive MOC|offensive team]].

## Related

- [[Web Application Security]]
- [[OWASP Top 10]]
- [[Firewall]]
- [[IDS and IPS]]
- [[Defences MOC]]
