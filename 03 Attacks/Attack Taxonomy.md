---
title: Attack Taxonomy
aliases: [Types of Attacks, Attack Classification]
category: attack
tags: [attack/overview, exam]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Attack Taxonomy

## Summary

There is no single correct classification of attacks — the useful lens depends on what you are doing. Defenders classify by **vector** (how it arrives), **objective** (what it breaks in the [[CIA Triad]]), or **technique** (what ATT&CK tactic it maps to). Attacks combine; a single incident is usually several of these stacked.

## By objective (CIA)

| Objective | Examples |
|---|---|
| Confidentiality | [[SQL Injection]], [[Man-in-the-Middle (MITM)]], [[Spyware and Keyloggers]], data exfiltration |
| Integrity | [[Cross-Site Scripting]], tampering, [[Ransomware]] (encryption = data destruction) |
| Availability | [[Denial of Service (DoS)]], [[Ransomware]], wipers, physical destruction |

## By vector

- **Network** — exposed services, [[Man-in-the-Middle (MITM)]], [[DNS Attacks]], [[Wireless Attacks]].
- **Application/web** — [[Injection Attacks]], [[Broken Access Control]], file upload, deserialisation.
- **Human** — [[Phishing]], [[Social Engineering]], [[Password Attacks]], vishing.
- **Host/endpoint** — malware, [[Privilege Escalation]], malicious macros, USB drops.
- **Supply chain** — dependencies, vendor access, build pipeline ([[Supply Chain Attack]]).
- **Physical** — tailgating, device theft, evil maid, rogue devices.

## By position relative to the defender

- **External** vs **internal** (insider, [[Lateral Movement]]).
- **Active** (scanning, exploitation) vs **passive** (eavesdropping, traffic analysis).
- **Opportunistic** vs **targeted** ([[Script Kiddie]] vs [[Advanced Persistent Threat]]).

## By mechanism

- **Exploiting a vulnerability** — memory corruption, logic flaw, misconfiguration.
- **Exploiting trust** — valid credentials, impersonation, [[Supply Chain Attack]].
- **Exploiting the human** — [[Social Engineering]].
- **Exploiting capacity** — [[Denial of Service (DoS)]].

Note the asymmetry: most real intrusions use *valid accounts* rather than a novel exploit. Hence identity is the modern perimeter.

## Phases (kill-chain view)

[[Reconnaissance]] → weaponisation → delivery → exploitation → installation → C2 → actions. See [[Cyber Kill Chain]] and [[MITRE ATT&CK]] for the granular version.

## Related

- [[Cyber Kill Chain]]
- [[MITRE ATT&CK]]
- [[OWASP Top 10]]
- [[Attacks MOC]]
