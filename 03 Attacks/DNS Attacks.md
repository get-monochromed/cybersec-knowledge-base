---
title: DNS Attacks
aliases: [DNS Spoofing, DNS Poisoning, DNS Tunnelling, DNS Hijacking]
category: attack
tags: [attack/network, dns]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# DNS Attacks

## Summary

DNS is unauthenticated by default, cached everywhere, and controls where traffic goes — so compromising it redirects, intercepts or hides traffic. It is also a reliable exfiltration channel.

## Techniques

- **Cache poisoning** — inject a forged answer into a resolver's cache; everyone using that resolver gets the attacker's IP for the TTL. Kaminsky-style attacks exploit transaction-ID/port prediction.
- **Spoofing (on-path)** — race the real response with a forged one on the local network; easy alongside [[ARP Spoofing]].
- **DNS hijacking** — modify registrar records, NS delegation, or router DNS settings; large-scale campaigns target home/office routers.
- **DNS tunnelling** — encode data in DNS queries/responses (TXT, NULL, long subdomains) to a C2 domain. Survives many egress filters because DNS is allowed.
- **Fast flux** — rapidly rotate A records among compromised hosts to keep malware infrastructure alive.
- **Domain fronting / domain shadowing** — hide C2 behind legitimate CDNs or compromised registrar accounts.
- **Subdomain takeover** — dangling CNAME to an unclaimed cloud resource; attacker claims it and serves content on your domain.
- **Typosquatting / homograph** — lookalike domains for phishing.
- **Zone transfer abuse** — misconfigured AXFR dumps the whole zone (recon).
- **DNS amplification** — spoofed queries to open resolvers, huge responses to the victim ([[Denial of Service (DoS)]]).
- **DNS rebinding** — change a hostname's IP to `127.0.0.1`/internal ranges to bypass same-origin protections against local services.

## Detection

- Resolver logs: high-volume TXT/NULL queries, long random subdomains, unusual query entropy, queries to newly registered domains.
- Response anomalies: TTL=0 or very low TTLs, mismatched authority, signed-zone failures.
- Certificate Transparency monitoring for your brand's lookalikes; registrar/NS change alerts.
- Dangling DNS records in an asset inventory (weekly automated check).

## Mitigation

- **DNSSEC** on your zones and validating resolvers — cryptographic answer integrity.
- **Encrypted DNS** (DoT/DoH) to prevent on-path spoofing (moves trust, does not remove it).
- **Registry/registrar locks**, MFA on registrar accounts, change alerting, DNSSEC key protection.
- **Egress DNS control**: internal resolvers only, block direct external DNS, log and baseline, flag tunnelling patterns.
- **Randomise source port + transaction ID** (resolver defaults) and patch resolvers.
- **Inventory DNS records**, remove dangling ones, monitor for takeover.
- **HSTS/CAA** and CT monitoring for impersonation.

## Related

- [[Man-in-the-Middle (MITM)]]
- [[ARP Spoofing]]
- [[Denial of Service (DoS)]]
- [[Phishing]]
- [[Attacks MOC]]
