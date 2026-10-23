---
title: Home
aliases: [Dashboard, Index, Start Here]
category: index
tags: [moc, home]
status: solid
created: 2026-10-23
updated: 2026-10-23
---

# Cyber Security Knowledge Base

Personal wiki of everything I know about cyber security. Start here, drill into a **MOC** (map of content), and follow the links.

## Sections

| # | Section | What lives here |
|---|---|---|
| 01 | [[Foundations MOC\|Foundations]] | CIA, AAA, principles, threat modelling, risk |
| 02 | [[Threats MOC\|Threats & Actors]] | Who attacks, why, and how we track them |
| 03 | [[Attacks MOC\|Attacks]] | Attack taxonomy and individual techniques |
| 04 | [[Malware MOC\|Malware]] | Malware families, analysis, detection |
| 05 | [[Defences MOC\|Defences]] | Controls: firewalls, IDS, EDR, access control |
| 06 | [[Domains MOC\|Domains]] | Network, web, cloud, mobile, OT, email |
| 07 | [[Offensive MOC\|Offensive Security]] | Pentest methodology, tooling, red teaming |
| 08 | [[Defensive Ops MOC\|Defensive Operations]] | SOC, IR, forensics, hunting, ATT&CK |
| 09 | [[GRC MOC\|Governance, Risk & Compliance]] | Standards, law, audits, policy |
| 10 | [[Cryptography MOC\|Cryptography]] | Primitives, PKI, TLS, PQC |
| 11 | [[Reference MOC\|Reference]] | Glossary, ports, tools, certs, cheatsheets |

## Quick jumps

**Concepts:** [[Kerberos]] · [[CIA Triad]] · [[Security Principles]] · [[Threat Modelling]] · [[Risk Management]] · [[Defence in Depth]] · [[Attack Surface]]

**Attacks:** [[Phishing]] · [[SQL Injection]] · [[Cross-Site Scripting]] · [[Denial of Service (DoS)]] · [[Man-in-the-Middle (MITM)]] · [[Ransomware]] · [[Privilege Escalation]] · [[Supply Chain Attack]]

**Defence:** [[Privileged Access Management]] · [[Firewall]] · [[IDS and IPS]] · [[WAF]] · [[Endpoint Protection]] · [[Access Control Models]] · [[Incident Response]] · [[SIEM]]

**Frameworks:** [[MITRE ATT&CK]] · [[NIST CSF]] · [[ISO 27001]] · [[CIS Controls]] · [[OWASP Top 10]]

**Crypto:** [[Symmetric Encryption]] · [[Asymmetric Encryption]] · [[Hashing]] · [[TLS]] · [[Digital Signatures and PKI]]

## Workflow

Drop raw notes, links and clippings into `Unorganised/` (or capture into [[Inbox]] via QuickAdd), then tell Pi to ingest. See [[README]] for conventions and [[AGENTS]] for the rules Pi follows.

## Vault health

Notes still needing work:

```dataview
LIST WHERE status = "stub" SORT file.mtime DESC LIMIT 25
```

Recently updated:

```dataview
TABLE status, category, file.mtime AS "Updated"
FROM "01 Foundations" OR "02 Threats" OR "03 Attacks" OR "04 Malware" OR "05 Defences" OR "06 Domains" OR "07 Offensive" OR "08 Defensive Ops" OR "09 GRC" OR "10 Cryptography" OR "11 Reference"
SORT file.mtime DESC
LIMIT 15
```

Total notes by section:

```dataview
TABLE length(rows) AS "Notes"
FROM "01 Foundations" OR "02 Threats" OR "03 Attacks" OR "04 Malware" OR "05 Defences" OR "06 Domains" OR "07 Offensive" OR "08 Defensive Ops" OR "09 GRC" OR "10 Cryptography" OR "11 Reference"
GROUP BY split(file.folder, "/")[0] AS Section
SORT Section ASC
```
