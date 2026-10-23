---
title: IoT Security
aliases: [Internet of Things Security, Embedded Security]
category: domain
tags: [domain/iot]
status: solid
up: "[[Domains MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# IoT Security

## Summary

Internet-connected devices with long lives, no patching culture, default credentials, and often no security team behind them. They are the raw material of [[Botnet|botnets]] and the easiest way into a corporate network from the "smart" side.

## Why it is hard

- **No update path** — firmware is rarely patched; EOL is measured in a decade.
- **Default/shared credentials**, telnet/SSH exposed, UPnP opening ports.
- **Constrained hardware** — no room for agents, EDR, or strong crypto.
- **Insecure supply chain** — firmware from third-party SDKs, no SBOM.
- **Physical exposure** — devices in public spaces, easy to access UART/JTAG.
- **Shadow IoT** — nobody knows how many devices exist ([[Attack Surface]]).

## Threat model

- Botnet recruitment ([[Denial of Service (DoS)]]), cryptomining, proxy.
- Pivot into the corporate LAN from a camera/printer/HVAC controller.
- Physical/sensor data manipulation.
- Privacy violations (cameras, microphones, location).

## Controls

- **Network isolation** — dedicated IoT VLAN/SSID, default deny to corporate, egress allow-list only ([[Network Segmentation]]).
- **No internet exposure** — never port-forward to a device; use outbound-only connections or a broker.
- **Credential hygiene** — change defaults at provisioning, unique per device, no shared passwords.
- **Asset inventory** — passive discovery (DHCP/DNS/ARP/802.1X) to find shadow devices.
- **Firmware policy** — vendor must support updates; verify signatures; track EOL.
- **Monitoring** — baseline behaviour; alert on new outbound destinations, telnet/SSH brute force, scanning.

## Regulation/standards

ETSI EN 303 645, UK PSTI Act, EU Cyber Resilience Act, US Cyber Trust Mark — the direction is mandated baseline security for consumer IoT. Enterprise: IEC 62443 for industrial devices ([[OT and ICS Security]]).

## Related

- [[Botnet]]
- [[Network Segmentation]]
- [[OT and ICS Security]]
- [[Attack Surface]]
- [[Domains MOC]]
