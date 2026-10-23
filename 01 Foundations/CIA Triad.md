---
title: CIA Triad
aliases: [CIA, Confidentiality Integrity Availability, AIC triad]
category: foundation
tags: [foundation/core, exam]
status: solid
up: "[[Foundations MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# CIA Triad

## Summary

The three properties information security exists to protect. Every control, attack and policy ultimately maps back to one of them, and the classic exam/interview opener is "which leg does this hurt, and what is the trade-off?"

## The three

| Property | Means | Broken by | Preserved by |
|---|---|---|---|
| **Confidentiality** | Only authorised parties can read the data | [[Man-in-the-Middle (MITM)]], [[SQL Injection]], data leaks, [[Spyware and Keyloggers]] | Encryption ([[Symmetric Encryption]], [[TLS]]), [[Access Control Models]], classification |
| **Integrity** | Data is accurate and unaltered, in transit and at rest | [[Man-in-the-Middle (MITM)]], malware tampering, unauthorised writes | [[Hashing]], [[Digital Signatures and PKI]], file integrity monitoring, versioning |
| **Availability** | Data and services are reachable when needed | [[Denial of Service (DoS)]], [[Ransomware]], hardware failure | Redundancy, [[Backup and Recovery]], [[Denial of Service (DoS)#Mitigation\|DDoS mitigation]] |

## How it is used

- **Threat modelling** starts by asking which leg each asset depends on.
- **Risk statements** name the affected leg: "loss of integrity on the payment ledger", not "a hack".
- **Control selection** targets the leg under threat — encryption does nothing for availability.

## Tensions (the interesting part)

- Confidentiality vs availability: aggressive encryption and key management can make recovery impossible after an outage.
- Integrity vs availability: strict integrity checks can block legitimate writes.
- Confidentiality vs usability: MFA and least privilege add friction, so they get bypassed if too heavy.
- Security vs privacy: monitoring to protect availability may violate confidentiality obligations (see [[GDPR]]).

## Extensions

Some models add **non-repudiation** (you cannot deny an action — see [[Digital Signatures and PKI]]) and **authenticity** (data really came from the claimed sender). **Parkerian hexad** adds possession/control and utility. **AAA** ([[Authentication, Authorization and Accounting]]) is the operational counterpart.

## Related

- [[Security Principles]]
- [[Vulnerability, Threat, Risk and Exploit]]
- [[Threat Modelling]]
- [[Security Controls]]
- [[Foundations MOC]]
