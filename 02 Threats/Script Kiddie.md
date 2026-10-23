---
title: Script Kiddie
aliases: [Skid, Script Kiddies, Unskilled Attacker]
category: actor
tags: [actor/low-capability]
status: solid
up: "[[Threats MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Script Kiddie

## Summary

Low-skill actor who runs existing tools and exploit kits without understanding them. Individually weak, collectively significant: automated scanning means *every* exposed service is tested continuously.

## Motivation

Fun, notoriety, "hacking" clout, low-effort fraud. Rarely targeted — opportunistic.

## Capability

- Uses pre-built: DDoS-for-hire (stressers), vulnerability scanners, default-credential lists, phishing kits, reverse shells from GitHub, Telegram-shared malware.
- Poor operational security: reuses infrastructure, leaks identity, fails at covering tracks.
- Cannot develop exploits, rarely persists against resistance.

## Typical TTPs

- Broad internet scanning → [[Scanning and Enumeration]]; attacking anything with a known CVE.
- Default and weak credentials → [[Password Attacks]]; exposed RDP/SSH.
- [[Phishing]] templates, defacement of unpatched CMS sites (WordPress plugins).
- [[Denial of Service (DoS)]] via rented booter services.

## Why they still matter

- Volume: they find the forgotten server, the dev environment with `admin:admin`.
- Because cheap: they are the source of most initial access that later gets sold to [[Cybercriminal|cybercriminals]].

## Defensive focus

Hygiene removes nearly all of their opportunity: patch, no default credentials, no exposed admin interfaces, MFA everywhere, [[Attack Surface]] reduction, basic [[IDS and IPS]]. They are the reason "boring" controls still top the risk list.

## Related

- [[Threat Actor]]
- [[Attack Surface]]
- [[Password Attacks]]
- [[Attack Taxonomy]]
- [[Threats MOC]]
