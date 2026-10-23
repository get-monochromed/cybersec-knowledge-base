---
title: Bug Bounty
aliases: [Bug Bounty Programme, VDP, Responsible Disclosure]
category: offensive
tags: [offensive/bounty, governance]
status: developing
up: "[[Offensive MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Bug Bounty

## Summary

Paying external researchers for vulnerabilities, under a published policy. Continuous, scalable testing that complements periodic pentests — but only if the programme is well scoped and triaged.

## Variants

- **VDP** (vulnerability disclosure programme) — no payment, safe harbour, thank-you. Cheap starting point.
- **Public bounty** — anyone can submit; high volume, high duplicate rate.
- **Private/invite-only** — vetted researchers; better signal for mature programmes.
- **Managed (platform)** — HackerOne, Bugcrowd, Intigriti, YesWeHack handle triage and payment.

## Policy contents

Scope (domains, apps, mobile, APIs), out-of-scope (DoS, social engineering, physical, third-party), safe harbour language, disclosure timeline, reward table, and rules on data handling. This is a form of [[Rules of Engagement]] — researchers must be able to rely on it legally.

## Operating it well

- **Triage fast** — slow triage kills researcher interest and delays fixes.
- **Pay for impact, not CVSS alone** — business logic and access-control bugs are worth more than a reflected XSS.
- **Avoid duplicates by design** — private programmes, clear scope, hints on what is already known.
- **Close the loop** — tell researchers what was fixed; publish a hall of fame.
- **Watch for scammers** — AI-generated low-quality reports are a real cost; require reproduction steps.
- **Budget for fixing**, not just paying: a bounty programme that generates findings nobody fixes is worse than none.

## Researcher side

Read the scope, respect rate limits, never access more data than needed to prove impact, report privately, do not go public before the agreed date. Duplicates and "won't fix" are normal; a good report is a clear reproduction, impact statement, and suggested fix.

## Related

- [[Penetration Testing]]
- [[Rules of Engagement]]
- [[Vulnerability Management]]
- [[Offensive MOC]]
