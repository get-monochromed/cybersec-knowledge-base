---
title: Domains MOC
aliases: [Domains, Security Domains, Disciplines]
category: index
tags: [moc]
status: solid
up: "[[Home]]"
created: 2026-10-23
updated: 2026-10-23
---

# Domains

Security applied to a specific technology stack. Each domain is a different threat model, a different set of controls, and often a different standard.

| Domain | Core risk | Key controls |
|---|---|---|
| [[Network Security]] | interception, exposure | firewalls, segmentation, TLS |
| [[Web Application Security]] | injection, access control | secure coding, WAF, SAST/DAST |
| [[Application Security]] | insecure SDLC | threat modelling, SCA, secure defaults |
| [[Cloud Security]] | misconfiguration, identity | CSPM, least-privilege IAM, logging |
| [[Container Security]] | image and runtime trust | minimal images, admission control |
| [[Operating System Security]] | privilege, patching | hardening, EDR, LAPS |
| [[Email Security]] | spoofing, phishing | SPF/DKIM/DMARC, filtering |
| [[Mobile Security]] | device loss, malicious apps | MDM, app vetting, encryption |
| [[IoT Security]] | default creds, no patching | network isolation, no internet exposure |
| [[OT and ICS Security]] | physical consequences | segmentation, passive monitoring |
| [[Wireless Security]] | rogue APs, weak crypto | WPA3-Enterprise, 802.1X |

## Related

- [[Attacks MOC]]
- [[Defences MOC]]
- [[GRC MOC]]
