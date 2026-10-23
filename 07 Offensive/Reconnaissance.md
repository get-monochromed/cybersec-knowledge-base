---
title: Reconnaissance
aliases: [Recon, OSINT, Information Gathering]
category: offensive
tags: [offensive/recon, osint]
status: solid
up: "[[Offensive MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Reconnaissance

## Summary

Mapping the target before touching it. Passive recon uses only public information (no direct interaction); active recon queries the target's systems and can be logged. Attackers do this continuously; the defender's equivalent is asset discovery and [[Attack Surface]] management.

## Passive (OSINT)

- **DNS** — WHOIS/RDAP, certificate transparency logs (crt.sh) for subdomains, passive DNS, zone data from third parties.
- **Search engines** — Google dorks (`site:`, `filetype:`, `inurl:`), GitHub/GitLab code search for leaked keys, `grep.app`.
- **Shodan/Censys/ZoomEye** — exposed services, banners, TLS certificates, default pages.
- **Social** — LinkedIn org chart (targets for [[Social Engineering]]), job ads revealing tech stack, conference talks, GitHub profiles.
- **Breach data** — credential exposure (HIBP), past leaks, paste sites.
- **Archives** — Wayback Machine for old endpoints and removed pages.
- **Metadata** — documents with author names, internal paths, software versions.

## Active

- DNS enumeration: `dig`, `dnsrecon`, `dnsx`, zone transfer attempts (`AXFR`).
- Subdomain brute force: `amass`, `subfinder`, `ffuf` with wordlists.
- Port scanning → [[Scanning and Enumeration]].
- Web content discovery: `ffuf`/`gobuster` against directories and vhosts.
- TLS certificate inspection for internal hostnames.

## What good recon produces

- Asset list with owners, technologies and versions.
- Named people with roles (for social engineering or phishing pretexts).
- Credential exposure and leaked secrets.
- Third parties and suppliers — often the weakest link ([[Supply Chain Attack]]).

## Defensive counterpart

You cannot defend unmanaged exposure: run the same enumeration against yourself (EASM), monitor certificate transparency for your domains, alert on new subdomains, and remove abandoned assets. Attackers' recon is your asset inventory gap.

## Related

- [[Scanning and Enumeration]]
- [[Attack Surface]]
- [[Social Engineering]]
- [[Security Tools]]
- [[Offensive MOC]]
