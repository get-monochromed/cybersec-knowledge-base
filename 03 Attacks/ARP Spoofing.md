---
title: ARP Spoofing
aliases: [ARP Poisoning, ARP Cache Poisoning]
category: attack
tags: [attack/network, lan]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# ARP Spoofing

## Summary

ARP has no authentication: any host can claim any IP. An attacker floods gratuitous ARP replies mapping the gateway's IP to their own MAC, so victims send their traffic to the attacker — a LAN-level [[Man-in-the-Middle (MITM)]].

## How it works

1. Attacker sends forged ARP replies: "192.168.1.1 is at aa:bb:cc:dd:ee:ff" (attacker MAC).
2. Victim's ARP cache updates; traffic to the gateway now goes to the attacker.
3. Attacker forwards packets (so the victim notices nothing) while sniffing or modifying.
4. Repeat for the gateway's cache to intercept return traffic — full bidirectional MITM.
5. Optional extras: session cookie theft, credential capture on plaintext protocols, DNS spoofing, SSL stripping.

## Variants

- **Gratuitous ARP poisoning** — unsolicited replies, fast and loud.
- **ARP request poisoning** — replies to legitimate requests.
- **MAC flooding** — overflow the switch's CAM table so it falls back to hub behaviour (flooding all frames).
- **DHCP starvation + rogue DHCP** — exhaust the pool, then hand out your own gateway/DNS.

## Detection

- **arpwatch** / IDS rules (Snort `arpspoof`, Suricata) alert on MAC-IP mapping changes.
- Duplicate MAC address seen on multiple switch ports; one MAC claiming many IPs.
- Gateway MAC changes unexpectedly.
- Traffic asymmetry: TTL anomalies, latency spikes, unexpected hops (`traceroute` on the LAN).
- Endpoint ARP table inspection (`arp -a`) — static entries that suddenly become dynamic are suspicious.

## Mitigation

- **Dynamic ARP Inspection (DAI)** with DHCP snooping on managed switches — the real fix at the network layer.
- **Port security** (limit MACs per port), 802.1X for port authentication.
- **Static ARP entries** for critical gateways on sensitive hosts (small environments).
- **Encryption everywhere** — TLS, SSH, IPsec, SMB signing — so interception yields ciphertext (defence in depth, not a fix).
- **Network segmentation** and private VLANs to limit the attack domain ([[Network Segmentation]]).
- Wireless: don't treat Wi-Fi as trusted; client isolation on guest networks.

## Related

- [[Man-in-the-Middle (MITM)]]
- [[DNS Attacks]]
- [[Network Segmentation]]
- [[Wireless Attacks]]
- [[Attacks MOC]]
