---
title: IT Act 2000
aliases: [Information Technology Act, IT Act, CERT-In Directions, Section 66]
category: grc
tags: [grc/law, india]
status: solid
up: "[[GRC MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: ["Information Technology Act, 2000 (India)", "CERT-In Directions, April 2022"]
---

# IT Act 2000

## Summary

India's primary cyber law (amended 2008). It creates offences for unauthorised access and damage, and provides the legal basis for incident reporting — most operationally important are the CERT-In directions under s.70B.

## Key provisions

| Section | Meaning |
|---|---|
| s.43 | Civil liability for damage to computer/data (unauthorised access, downloading, disruption) |
| s.43A | Body corporate duty to protect sensitive personal data (largely superseded by [[DPDP Act 2023]]) |
| s.65 | Tampering with computer source code |
| s.66 | Computer-related offences (dishonest/fraudulent acts) |
| s.66B | Receiving stolen computer resource |
| s.66C | Identity theft |
| s.66D | Cheating by personation (fake profiles) |
| s.66E | Privacy violation (publishing private images) |
| s.66F | Cyber terrorism |
| s.67 | Obscene material |
| s.69 | Government interception/decryption powers |
| s.70 | Protected systems (critical information infrastructure) |
| s.72 | Breach of confidentiality by persons with lawful access |

## CERT-In directions (April 2022) — operationally critical

- Report **cyber security incidents within 6 hours** of noticing them (specified incident types).
- Maintain **logs for 180 days** within India.
- Synchronise ICT system clocks to NTP (NIC/NPL).
- Submit **point-of-contact** details and KYC/records for cloud, VPN, crypto services.
- Enable **encryption of data at rest** and maintain a 5-year KYC record for subscribers of specified services.
- Respond to CERT-In information requests.

These obligations drive architecture: log retention and local storage are compliance requirements, not just IR preferences ([[SIEM]]).

## Other pieces

- **SPDI Rules 2011** — sensitive personal data handling (being replaced by the DPDP framework).
- **Intermediary Guidelines (2021)** — safe harbour conditions for platforms.
- **NCIIPC** — protects Critical Information Infrastructure under s.70.

## Related

- [[DPDP Act 2023]]
- [[Incident Response]]
- [[Compliance Audit]]
- [[GRC MOC]]
