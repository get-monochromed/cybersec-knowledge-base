---
title: EternalBlue
aliases: [EternalBlue (NSA), MS17-010, CVE-2017-0144, ETERNALBLUE]
category: attack
tags: [attack/network, attack/host, smb, nsa, exam]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-24
updated: 2026-10-24
sources: ["Wikipedia: EternalBlue (clipping, ingested 2026-10-24)", "Microsoft security bulletin MS17-010", "NVD CVE-2017-0144"]
---

# EternalBlue

## Summary

A remote, unauthenticated exploit for Microsoft's SMB version 1 (SMBv1) server, written by the U.S. National Security Agency (NSA) and leaked publicly in April 2017. It turns any reachable, unpatched Windows host into a SYSTEM-level remote code execution target in a single packet — which is why it became the engine of [[WannaCry]] and [[NotPetya]], and the textbook case of a stockpiled vulnerability escaping into the wild.

It matters less as a CVE than as an argument: a state held a working exploit for an unpatched flaw for over five years, lost it, and the loss caused billions of dollars of damage to parties who had no say in the decision (see [[Vulnerability Disclosure]]).

## How it works

1. **Reachability** — attacker can open TCP 445 to the target's SMBv1 listener. No credentials, no user interaction.
2. **Trigger** — a crafted SMB packet sequence drives the SMBv1 server into mishandling its own packet parsing; the version 1 implementation is the flaw (SMBv2/v3 are not affected).
3. **Corruption** — kernel pool memory in the SMBv1 driver (`srv.sys`) is corrupted, giving a controlled write primitive.
4. **Execution** — the exploit shapes the pool to achieve arbitrary code execution at `NT AUTHORITY\SYSTEM`.
5. **Payload** — anything: a backdoor, a credential dumper, or a self-propagating [[Worm]] copy.

- **CVE** — CVE-2017-0144
- **Vendor bulletin** — MS17-010, released Patch Tuesday 14 March 2017
- **Affected at disclosure** — Windows Vista, 7, 8.1, 10, Server 2008, 2008 R2, 2012, 2012 R2, 2016. Emergency builds followed for Windows XP, Windows 8 and Server 2003.
- **Port** — 445/tcp (139 via NetBIOS); see [[Ports and Protocols]]

## Timeline

| Date | Event |
|---|---|
| ~2012–2017 | NSA holds the flaw and the exploit; Microsoft is not told. Notified only after the theft, so MS17-010 could be prepared |
| Mar 2016 | Buckeye (APT3) reportedly uses EternalBlue — likely independently found or re-purposed |
| 14 Mar 2017 | MS17-010 patches released for supported Windows versions |
| 14 Apr 2017 | The Shadow Brokers publish EternalBlue with other NSA tooling after an unsold auction |
| 12 May 2017 | [[WannaCry]] uses it to spread globally as ransomware |
| 13 May 2017 | Microsoft ships emergency patches for unsupported XP, Windows 8 and Server 2003 |
| 27 Jun 2017 | [[NotPetya]] uses it for lateral spread during the Ukraine-centred attack |
| Feb 2018 | RiskSense ports EternalBlue (and EternalChampion, EternalRomance) to every Windows since 2000; released as Metasploit modules |
| Late 2018 | Millions of hosts still unpatched; BadRabbit and Retefe also use it |
| 2019 | City of Baltimore attack blamed on it — attribution retracted, see below |

## Variants and related tooling

- **EternalChampion / EternalRomance** — other SMB exploits from the same leak, ported alongside it.
- **EternalRocks** — a worm that chains seven leaked NSA exploits, installs Tor for command and control (C2), waits 24 hours, then drops payloads. First found via a [[Honeypot]]. It masquerades as WannaCry in its file properties and has no kill switch and no ransomware payload. See [[Worm]].
- **Metasploit `ms17_010_eternalblue`** and derivatives — commodity-grade by 2018, so script-kiddie reachable.

## Detection

- **SMBv1 traffic at all** — there is no good reason for it on a modern network; treat the protocol's presence as the finding, not just the exploit.
- **Vulnerability scan** — `nmap --script smb-vuln-ms17-010`, or an authenticated scanner's MS17-010 plugin ([[Vulnerability Management]]).
- **IDS/IPS signatures** for the exploit's SMB transaction pattern; these exist for every mainstream engine, but encryption and evasion reduce reliability.
- **Endpoint** — unexpected `SYSTEM`-context process creation, service creation, `\\host\ADMIN$` writes, credential dumping.
- **Fan-out** — one host opening 445 to many peers in a short window is a worm, and is the highest-fidelity signal ([[Worm]], [[Lateral Movement]]).

## Mitigation

1. **Disable SMBv1** everywhere. This removes the attack surface outright and is the durable fix; patching alone leaves you one missed host away from reinfection ([[Hardening]]).
2. **Patch MS17-010** — and keep patching: the exploit was re-ported to every Windows generation, so "we're not on 7" is not immunity ([[Patch Management]]).
3. **Block 445/139 at network boundaries**, never expose SMB to the internet, and default-deny inbound on host firewalls.
4. **Segment** so a single infected host cannot reach thousands of peers ([[Network Segmentation]]).
5. **[[Endpoint Protection|EDR]]** with behaviour rules for credential dumping and remote service creation — the window between exploit and encryption.
6. **Assume legacy exists**: medical devices, manufacturing controllers and OT networks often cannot be patched; isolate them instead ([[OT and ICS Security]]).

## Impact

- WannaCry: attributed over US$8 billion in damages across 150 countries — **figures flagged below**.
- NotPetya: White House assessment of more than US$10 billion; the most destructive cyberattack on record by business impact.
- Both reached critical national infrastructure: NHS trusts, Ukraine's ministries and banks, Chernobyl's radiation monitoring, Maersk, FedEx, Merck.

> [!warning] Unverified — WannaCry figures
> The clipping states WannaCry caused "over $8 billion in damages across 150 countries" and that "over 36,000 computers were infected" (Avast, citing Russia, Ukraine and Taiwan as the majority). The infection count is far below the ~200,000–300,000 figure usually cited, and is best read as a point-in-time count from one vendor rather than a total. Treat both numbers as approximate and unattributed until checked against the primary sources.

### Baltimore, May 2019 — a retracted attribution

The clipping records that *The New York Times* initially attributed Baltimore's ransomware attack to EternalBlue, and that the same reporter (Nicole Perlroth, in a 2021 book) later clarified EternalBlue **was not** responsible — while criticising people who fixated on the technical detail that the ransomware had not spread that way.

> [!warning] Unverified — attribution
> The retraction is carried here as the source's own correction; no independent confirmation of either position was available in the clipping. Do not use Baltimore as an EternalBlue case study.

The defensible lesson from Baltimore is the one researchers made at the time: substantial numbers of Windows machines two years without patches is the organisation's failure, not the exploit's novelty ([[Patch Management]], [[Risk Management]]).

## Responsibility and the disclosure debate

Microsoft accepted responsibility for patching but publicly criticised U.S. intelligence agencies for **stockpiling** flaws instead of disclosing them, comparing it to the military having Tomahawks stolen. Critics of Microsoft (e.g. Alex Abdo, Knight First Amendment Institute) replied that the vendor remains accountable for shipping a vulnerable product and for limiting the first patch round to supported and paid Extended Support customers — which left bodies like the UK's NHS exposed.

Both critiques are load-bearing and neither is complete; see [[Vulnerability Disclosure]] for the policy mechanics (VEP, coordinated disclosure, disclosure deadlines).

## Related

- [[WannaCry]]
- [[NotPetya]]
- [[Petya]]
- [[Worm]]
- [[Vulnerability Disclosure]]
- [[Lateral Movement]]
- [[Patch Management]]
- [[Attacks MOC]]
