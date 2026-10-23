---
title: Wireless Security
aliases: [Wi-Fi Security, WPA3, 802.1X, WLAN Security]
category: domain
tags: [domain/wireless, network]
status: solid
up: "[[Domains MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Wireless Security

## Summary

Protecting 802.11 networks and the devices on them. The radio is shared, so assume anyone in range can listen and inject — security comes from strong cryptography, mutual authentication, and treating Wi-Fi as untrusted transport.

## Standards

| Standard | Crypto | Verdict |
|---|---|---|
| WEP | RC4, 24-bit IV | broken, minutes |
| WPA (TKIP) | RC4/TKIP | deprecated, broken |
| WPA2-Personal | AES-CCMP, PSK | fine if passphrase strong; offline crackable |
| WPA2-Enterprise | 802.1X + EAP-TLS | good, needs client cert validation |
| WPA3-Personal | SAE (dictionary-resistant) | good, prefer this |
| WPA3-Enterprise | 192-bit suite | best for corporate |
| OWE | opportunistic encryption on open networks | better than open |

## Enterprise design

- **WPA3-Enterprise (or WPA2-Enterprise) with EAP-TLS** — server certificate validation on clients is the control that stops [[Wireless Attacks|evil twins]].
- **802.1X + RADIUS** for port/NAC; dynamic VLAN assignment per role.
- **Separate SSIDs/VLANs**: corporate, guest (isolated), IoT (isolated, egress-limited), OT (no wireless).
- **PMF (802.11w)** enabled; WPS disabled; management frames protected.
- **AP hardening**: patched firmware, no default admin creds, management on a dedicated VLAN, no rogue APs.

## Operations

- **WIDS/WIPS** for rogue AP and evil twin detection; periodic site surveys.
- **Guest onboarding** with sponsor approval, time-limited credentials.
- **Certificate lifecycle** for EAP-TLS (SCEP/EST, revocation).
- Treat wireless as untrusted: VPN/ZTNA to internal resources, not direct access ([[Zero Trust Architecture]]).

## Related

- [[Wireless Attacks]]
- [[Network Security]]
- [[Network Segmentation]]
- [[Domains MOC]]
