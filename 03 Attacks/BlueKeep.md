---
title: BlueKeep
aliases: [BlueKeep, CVE-2019-0708, MS19-0708]
category: attack
tags: [attack/network, attack/host, rdp, microsoft]
status: developing
up: "[[Attacks MOC]]"
created: 2026-10-24
updated: 2026-10-24
sources: ["Wikipedia: BlueKeep (clipping, ingested 2026-10-24)"]
---

# BlueKeep

## Summary

A pre-authentication remote code execution vulnerability in Microsoft's Remote Desktop Protocol (RDP) service, disclosed and patched in May 2019 and tracked as **CVE-2019-0708**. It matters because of what it combines: no credentials required, no user interaction, and execution at **system level** — the same profile as [[EternalBlue]], which is why it was treated as a potential worm rather than a routine RDP flaw.

It is also a case study in patching the unpatachable: Microsoft shipped fixes for Windows XP, Vista and Server 2003, all long past end-of-life and otherwise ineligible for updates.

> [!warning] Unverified — "DejaBlue" naming
> The source file was named `DejaBlue(BlueKeep).md`, but its content describes **only** CVE-2019-0708 (patched 14 May 2019). "DejaBlue" is normally used for the separate set of RDP vulnerabilities Microsoft disclosed in **August 2019** (CVE-2019-1181 / CVE-2019-1182 and relatives). The two are different bugs in the same service and are **not** aliased together here. If the vault later needs the August 2019 set, create a separate note rather than extending this one.

## How it works

1. **Virtual channels** — RDP multiplexes "virtual channels" between client and server as an extensible data path, configured **before authentication** completes. RDP 5.1 defines 32 **static** channels; **dynamic** channels are carried inside one of those static channels.
2. **The bad binding** — the server binds a channel named `MS_T120` to a static channel. There is no legitimate reason for a client to connect to `MS_T120`, and it is not supposed to be bound below channel 31.
3. **Trigger** — a client requests `MS_T120` bound to a static channel **other than 31**. The server honours the request.
4. **Consequence** — the mis-binding causes **heap corruption**, which the attacker shapes into **arbitrary code execution at system level** — all before any credential exchange.

The pre-auth position is the whole point: RDP brute-force defences, NLA enforcement and password policy are irrelevant to it.

## Affected systems

| Status | Versions |
|---|---|
| Vulnerable | Windows XP, Vista, 7, Server 2003, Server 2008, Server 2008 R2 |
| Not affected | Windows 8, 10, 11 and newer |
| Additional | CISA reported it also achieved code execution on Windows 2000 |

The vulnerable set is precisely the estate that cannot be patched quickly: clinical devices, industrial HMIs, kiosks and embedded terminals running Windows 7 or XP with RDP left enabled for vendor support.

## Detection

- **3389/tcp exposed to the internet** — the precondition for mass exploitation; enumerate it ([[Attack Surface]], [[Scanning and Enumeration]]).
- **RDP scanning and exploit attempts** — connection attempts that fail before authentication, or unusually crafted `MS_T120` channel requests, visible in IDS/honeypot telemetry ([[Honeypot]], [[IDS and IPS]]).
- **Vulnerability scan** — authenticated scans and MS19-0708/CVE-2019-0708 plugins; unauthenticated scans still identify the version fingerprint ([[Vulnerability Management]]).
- **Crash pattern** — `termdd.sys` bugcheck / unexpected RDP service termination on hosts under probing.
- **Legacy OS presence at all** — XP/2003/2008 in the asset inventory is the finding that makes the CVE urgent ([[Attack Surface]]).

## Mitigation

1. **Patch** — 14 May 2019 builds, including the out-of-band XP/Vista/Server 2003 packages. The fix forces `MS_T120` to always bind to channel 31, even if the server is asked otherwise ([[Patch Management]]).
2. **Take RDP off the internet.** Sophos' position, and the correct one: switch RDP off if it is not needed; if it is needed, expose it only through a VPN or a brokered zero-trust path ([[VPN]], [[Zero Trust Architecture]]).
3. **Disable Remote Desktop Services and close 3389** where unused — the NSA's first recommendation ([[Hardening]], [[Ports and Protocols]]).
4. **Require Network Level Authentication (NLA)** — it does not stop BlueKeep (the bug is pre-auth), but it removes a large class of RDP abuse around it.
5. **Two-factor authentication** on RDP access; Sophos argued it may reduce the practical risk of RDP compromise generally ([[Authentication, Authorization and Accounting]], [[Privileged Access Management]]).
6. **Segment** so an RDP compromise on a kiosk cannot reach the domain ([[Network Segmentation]]).
7. **Isolate what cannot be patched** — allow-list the vendor's support path instead of leaving 3389 open ([[OT and ICS Security]]).

## Why it is studied alongside EternalBlue

| | [[EternalBlue]] (2017) | BlueKeep (2019) |
|---|---|---|
| Service | SMBv1, 445/tcp | RDP, 3389/tcp |
| Authentication | none | none (pre-auth) |
| Impact | SYSTEM RCE | SYSTEM RCE |
| Patch reach | all supported, later EOL builds | all vulnerable, including EOL builds |
| Wormable? | yes — weaponised within weeks | yes in principle; no mass worm observed |
| Failure mode | patch lag on servers | patch lag on devices nobody can reboot |

The last row is the difference: EternalBlue exposed neglected servers, BlueKeep exposed neglected **appliances**. Different inventory problem, same outcome ([[Vulnerability Management]]).

## Related

- [[EternalBlue]]
- [[Patch Management]]
- [[Ports and Protocols]]
- [[VPN]]
- [[Network Segmentation]]
- [[Exploitation]]
- [[Lateral Movement]]
- [[Attacks MOC]]
