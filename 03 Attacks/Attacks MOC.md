---
title: Attacks MOC
aliases: [Attacks, Attack Types]
category: index
tags: [moc]
status: solid
up: "[[Home]]"
created: 2026-10-23
updated: 2026-10-23
---

# Attacks

Attack techniques, grouped by where they act. Each note follows Summary → How it works → Variants → Detection → Mitigation.

## Framing

- [[Attack Taxonomy]] — how attacks are classified
- [[Cyber Kill Chain]] — the phases of an intrusion
- [[MITRE ATT&CK]] — the technique catalogue
- [[OWASP Top 10]] — web risk ranking

## Social / human

- [[Phishing]] — by far the most common initial access
- [[Business Email Compromise]] — money, not malware
- [[Social Engineering]] — pretexting, tailgating, helpdesk abuse
- [[Password Attacks]] — spraying, stuffing, brute force

## Active Directory / Kerberos

- [[Kerberos]] (foundations) — the ticket flow everything below abuses
- [[Kerberoasting]] — crack service tickets offline, any domain user
- [[AS-REP Roasting]] — accounts without pre-auth, username is enough
- [[Pass-the-Hash]] — NTLM hash reuse; why local admin reuse is fatal
- [[Golden Ticket]] — forged TGT from the krbtgt hash
- [[Silver Ticket]] — forged service ticket, invisible to the DC
- [[DCSync]] — replicate secrets from a DC using legitimate protocol
- [[Kerberos Delegation]] — unconstrained, constrained and RBCD abuse
- [[Active Directory Certificate Services (ADCS)]] — ESC1 and friends: certificates as credentials

## Web / application

- [[Injection Attacks]] — the family; SQLi, command, LDAP, template
- [[SQL Injection]] · [[Cross-Site Scripting]] · [[Cross-Site Request Forgery]]
- [[Broken Access Control]] — IDOR and friends; OWASP #1
- [[Session Hijacking]] — stealing the authenticated state

## Network

- [[Denial of Service (DoS)]] — availability attacks
- [[Man-in-the-Middle (MITM)]] — interception
- [[ARP Spoofing]] · [[DNS Attacks]] — local and name resolution
- [[Wireless Attacks]] — Wi-Fi specific

## Host / post-exploitation

- [[Privilege Escalation]] · [[Lateral Movement]] · [[Living off the Land]]
- [[Post Exploitation]] — the full methodology

## Supply chain

- [[Supply Chain Attack]] — trust in dependencies, vendors, build systems

## Related

- [[Threats MOC]] — who does this
- [[Defences MOC]] — what stops it
- [[Offensive MOC]] — how it is tested
