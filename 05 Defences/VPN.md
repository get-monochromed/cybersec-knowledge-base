---
title: VPN
aliases: [Virtual Private Network, IPsec, WireGuard, SSL VPN]
category: defence
tags: [defence/network, remote-access]
status: solid
up: "[[Defences MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# VPN

## Summary

An encrypted tunnel between a client and a network, historically the standard remote-access control. Still common, but increasingly replaced by ZTNA because a VPN grants *network* access — which is precisely what an attacker who steals credentials wants.

## Types

- **Remote access** — client → gateway (IPsec IKEv2, SSL/TLS VPN, WireGuard, OpenVPN).
- **Site-to-site** — office ↔ office, cloud ↔ datacentre.
- **Client-to-site with split tunnelling** — only corporate traffic goes through (more convenient, less visibility).
- **Mesh** — WireGuard/Tailscale-style, peer-to-peer with identity.

## Security issues

- **VPN appliances are a top initial-access vector** — repeated critical CVEs in Fortinet, Pulse Secure, Citrix, Ivanti. Pre-auth RCE in an internet-facing box that sits inside the perimeter.
- **Credential theft** — phished VPN creds without MFA are game over; even with MFA, AiTM/[[Session Hijacking]] applies.
- **Flat access** — once connected, the user can reach the whole internal network ([[Lateral Movement]], [[Zero Trust Architecture|zero trust]] as the fix).
- **Split tunnelling** — bypasses corporate inspection; malware talks directly to the internet.
- **Always-on expectation** — users disable it when it is slow.

## Hardening

- Patch immediately; treat VPN appliances as critical assets with an owner and an exposure review.
- **MFA on every VPN login**, phishing-resistant where possible; per-user certificates.
- **Per-app / least-privilege access**, not full network routes; restrict by group.
- Log authentication and session activity to [[SIEM]]; alert on impossible travel and off-hours logins.
- Segment the VPN pool into its own zone; no direct access to management networks.
- Consider **ZTNA** instead: per-application access with device posture, no network-level grant.

## Related

- [[Zero Trust Architecture]]
- [[Network Segmentation]]
- [[Man-in-the-Middle (MITM)]]
- [[Wireless Attacks]]
- [[Defences MOC]]
