---
title: Mobile Security
aliases: [Mobile Device Security, BYOD, MDM]
category: domain
tags: [domain/mobile]
status: solid
up: "[[Domains MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Mobile Security

## Summary

Phones and tablets hold the strongest authentication factors (SMS OTP, authenticator apps, passkeys) and the most personal data, while being the hardest devices to monitor. Mobile compromise therefore often means compromise of everything else.

## Threat model

- **Device loss/theft** — encryption and remote wipe are the controls.
- **Malicious/fleeceware apps** — over-permissioned apps, sideloaded APKs, fake banking apps.
- **OS vulnerabilities** — zero-click implants (Pegasus-class) for high-value targets.
- **Network** — hostile Wi-Fi, rogue APs ([[Wireless Attacks]]), but TLS blunts most of it.
- **Phishing on mobile** — harder to inspect URLs, easier to mis-tap ([[Phishing]]).
- **MDM/profile abuse** — malicious configuration profiles, enterprise sideloading.
- **Data leakage** — chat apps, screenshots, cloud backup of work data.

## Controls

- **MDM/UEM**: enforce encryption, passcode, OS version floor, jailbreak/root detection, app allow-lists, remote wipe, separation of work/personal (Android work profile, iOS managed apps).
- **App vetting** — official stores only for high-risk users, no sideloading, review permissions.
- **OS updates** — enable automatic updates; track EOL devices.
- **High-risk users**: iOS Lockdown Mode, Android Advanced Protection, hardware security keys, no SMS OTP.
- **Network**: per-app VPN or ZTNA, certificate pinning in apps, no open Wi-Fi without VPN.
- **MFA design**: prefer push/passkeys over SMS (SIM swap, SS7).

## Detection

- MDM compliance drift, jailbreak detections, unusual data usage/battery (spyware heuristic).
- Identity logs: sign-ins from new devices/locations ([[Session Hijacking]]).
- EMM alerts on sideloaded apps or removed profiles.

## Related

- [[Wireless Attacks]]
- [[Passkeys]]
- [[Authentication, Authorization and Accounting]]
- [[Spyware and Keyloggers]]
- [[Domains MOC]]
