---
title: Man-in-the-Middle (MITM)
aliases: [MITM, MitM, On-Path Attack, Eavesdropping]
category: attack
tags: [attack/network, confidentiality, exam]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Man-in-the-Middle (MITM)

## Summary

The attacker positions themselves between two parties and relays (or alters) their traffic. Modern name: *on-path attack*. Nearly always a prerequisite for something else — credential theft, session theft, code injection, downgrade.

## How it works

1. Get on-path: ARP spoofing on a LAN ([[ARP Spoofing]]), rogue Wi-Fi AP, DNS spoofing ([[DNS Attacks]]), BGP hijack, compromised router/ISP, or a malicious proxy.
2. Intercept: sniff plaintext, or terminate TLS with a forged certificate the client mistakenly trusts.
3. Act: steal credentials/cookies, modify content, downgrade to HTTP, inject code.

## Variants

- **ARP spoofing** — poison the LAN's ARP tables so traffic flows through the attacker.
- **DNS spoofing/poisoning** — return attacker IPs for legitimate names.
- **Rogue access point / evil twin** — a lookalike SSID, often with a captive portal that harvests credentials.
- **SSL stripping** — keep the client on HTTP, talk HTTPS to the server; defeated by HSTS.
- **TLS interception proxies** — corporate MITM with an installed root CA (legitimate tool, same technique).
- **BGP hijacking** — route-level interception at internet scale.
- **AiTM phishing proxies** — application-layer MITM that relays the real site and steals the post-MFA session.
- **Malicious browser extension / proxy** — intercepts inside the browser.

## Detection

- Certificate anomalies: unexpected issuer, self-signed, wrong hostname, pinning failures (mobile apps complain loudly).
- ARP: duplicate MACs for the gateway, ARP table flaps (arpwatch), gratuitous ARP bursts.
- DNS: responses with short TTLs from odd servers, mismatched authoritative answers.
- Network: asymmetric routing, unexpected TLS termination points, HTTP downgrade redirects.
- Endpoint: new root CA installed, proxy settings changed unexpectedly.

## Mitigation

- **TLS everywhere with validation**: HSTS, certificate pinning (mobile), OCSP stapling, no user-clickable cert bypasses.
- **HSTS preload** kills SSL stripping.
- **Encrypted DNS** (DoH/DoT) and DNSSEC reduce spoofing value.
- **Switch port security**: dynamic ARP inspection, DHCP snooping, static ARP for gateways, 802.1X.
- **Enterprise Wi-Fi**: WPA2/3-Enterprise with certificate validation, no open networks for corporate devices.
- **VPN** on untrusted networks — but remember a VPN moves the trust point, it does not eliminate it.
- **Phishing-resistant MFA** for the application-layer variant ([[Phishing]]).

## Related

- [[ARP Spoofing]]
- [[DNS Attacks]]
- [[Wireless Attacks]]
- [[TLS]]
- [[Session Hijacking]]
- [[Attacks MOC]]
