---
title: Wireless Attacks
aliases: [Wi-Fi Attacks, WPA Cracking, Evil Twin]
category: attack
tags: [attack/wireless, network]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Wireless Attacks

## Summary

Attacks against 802.11 networks. The radio medium is shared, so the attacker can listen, inject and impersonate without physical access — and users cannot see the difference between your AP and theirs.

## Techniques

- **WEP cracking** — RC4 with IV reuse; breakable in minutes. Legacy only.
- **WPA/WPA2-PSK offline cracking** — capture the 4-way handshake (or PMKID) and crack the passphrase offline. Strength of the passphrase is everything.
- **WPS PIN attack** — 8-digit PIN, often brute-forceable (Pixie Dust); disable WPS entirely.
- **Evil twin / rogue AP** — clone the SSID with a stronger signal, often with a captive portal to harvest credentials or serve a fake update.
- **Deauthentication attack** — forge deauth frames to disconnect clients; used to force reconnection to the evil twin or capture handshakes. (802.11w/PMF mitigates.)
- **KRACK** — key reinstallation against WPA2; patched in modern clients.
- **WPA3 downgrade / Dragonblood** — force clients to WPA2 or exploit SAE implementation flaws; patched where vendors updated.
- **Karma / known-beacon attacks** — respond to any SSID a device probes for.
- **Bluetooth/BLE attacks** — bluejacking, bluesnarfing, BLE spoofing, mousejack.
- **Rogue device on the LAN** — a Raspberry Pi hidden in a meeting room (physical).

## Detection

- Wireless IDS/IPS (WIDS/WIPS): rogue AP detection, evil-twin SSID with different BSSID, deauth floods.
- AP inventory reconciliation: unknown BSSIDs in your space.
- Client-side: certificate validation failures on 802.1X (users clicking through = red flag).
- DHCP anomalies and duplicate gateway MACs after association ([[ARP Spoofing]]).

## Mitigation

- **WPA3-SAE** (or WPA2-Enterprise with **EAP-TLS**), never PSK for corporate.
- **802.1X with server certificate validation** on clients — this is what defeats evil twins.
- **Protected Management Frames (802.11w)** to stop deauth abuse.
- **Disable WPS**, change default admin credentials on APs, patch firmware.
- **Separate SSIDs/VLANs**: guest isolated, IoT isolated, corporate separate ([[Network Segmentation]]).
- **WIDS/WIPS** and periodic rogue-AP sweeps.
- **Strong passphrases** where PSK is unavoidable; rotate after staff departures.
- Treat wireless as untrusted: VPN/ZTNA to internal resources ([[Zero Trust Architecture]]).

## Related

- [[Man-in-the-Middle (MITM)]]
- [[Network Segmentation]]
- [[Wireless Security]]
- [[Attacks MOC]]
