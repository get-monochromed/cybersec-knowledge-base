---
title: Spamhaus Project
aliases: [Spamhaus, The Spamhaus Project, Spamhaus Technology]
category: defence
tags: [defence/email, reputation, threat-intel]
status: developing
up: "[[Defences MOC]]"
created: 2026-10-24
updated: 2026-10-24
sources: ["[[_Archive/2026-10-24-spamhaus-project]]"]
---

# Spamhaus Project

## Summary

An international anti-spam organisation, founded in 1998 by Steve Linford and based in Andorra, that tracks email spammers and spam-supporting infrastructure. Its output is data, not software: anti-spam **DNS blocklists (DNSBLs)** that ISPs and mail servers query to reject or score mail before delivery. The name is a pseudo-German coinage by Linford for a "spam house" — an ISP or firm that spams or knowingly provides service to spammers.

The lists matter operationally for two reasons. First, they are one of the few shared reputation controls in email, so a listing can break deliverability for a whole network overnight. Second, the same data doubles as threat intelligence: compromised hosts, botnet command-and-control hosting, stolen netblocks and abused URL shorteners.

## Lists

| List | Type | Targets |
|---|---|---|
| **SBL** | IP | Verified spam sources: spammers, spam gangs, spam-support services. Partly derived from ROKSO. |
| **XBL** | IP | Illegal third-party exploits: open proxies, worms/viruses with built-in spam engines, infected PCs and servers, trojan exploits. Includes third-party input such as the Composite Blocking List (CBL). |
| **PBL** | IP | Addresses that should not send mail directly to third parties: dynamic ranges, plus static assignments such as ISP core routers, corporate users policy-bound to relay via company servers, and unassigned space. Data largely supplied by the ISPs that control the space. |
| **DBL** | Domain | Released March 2010. Both a domain/URI blocklist and an RHSBL: spam domains, payload URLs, spam senders, known spam gangs, phish/virus/malware sites. Later gained a zone for abused URL shorteners. |
| **CSS** | IP | Automatically generated low-reputation senders: HELO without an A record, generic-looking rDNS, fake domains — spambot behaviour or plain misconfiguration. Part of SBL. |
| **ZEN** | IP (composite) | Combined list: all Spamhaus IP-based DNSBLs. |
| **BCL** | IP | Released June 2012. Addresses believed to be operated by criminals exclusively to host botnet C2 infrastructure. |
| **DROP** | CIDR/ASN | "Don't Route Or Peer" — JSON files of netblocks and ASNs that are stolen or wholly spam-operated. A subset of SBL, excluding ISP ranges merely sublet to spammers, intended for firewalls and routers to drop traffic to and from the listed blocks entirely. Free to download; a BGP feed of the same data was offered from 2012. |
| **ROKSO** | Database | Register of Known Spam Operations: spammers and operations terminated by three or more ISPs. Not a DNSBL — public records of persons, domains, addresses and aliases. |

> [!warning] Unverified
> The clipping says ROKSO "stopped being available to the public at some point after 2023", citing two references that were lost in the capture. Treat the date and the current access model as unconfirmed; what is stated is that a law-enforcement version exists containing evidence, logs and detail on hundreds of spam gangs.

> [!warning] Unverified
> ZEN's exact composition is ambiguous in the source. It is described both as containing "all" Spamhaus IP-based DNSBLs and as including SBL — while CSS is separately described as part of SBL. Whether ZEN literally includes XBL, PBL and the CSS subset should be checked against current Spamhaus documentation before relying on it.

## Distribution and licensing

- Free public service for low-volume mail server operators.
- Commercial spam-filtering services and other large-scale users must hold a commercial account through Spamhaus Technology, its distribution partner.
- The filtering model is documented in Spamhaus's "Understanding DNSBL Filtering".
- 2006 figure: the services protected 650 million email users, including the European Parliament, the US Army, the White House and Microsoft, from billions of messages a day.

> [!warning] Unverified
> The 650-million-user figure is a 2006 claim by the organisation, not a current measurement. It is kept as historical context only.

## Limitations

- **Coarse granularity.** Listings are per IP, netblock, ASN or domain; a shared host or NAT pool inherits its neighbours' reputation.
- **False positives are expensive.** A listing affects all mail from that address, so delisting disputes and monitoring are part of operating a mail server.
- **DROP is narrow by design.** It covers only wholly-spam network blocks, so ranges sublet to spammers still need reputation scoring rather than a blanket drop.
- **Adversary turnover.** Spam infrastructure rotates to fresh ranges and domains, which is why CSS is generated automatically and DBL tracks abused shorteners.

> [!warning] Unverified
> The clipping captured no source URL, retrieval date or article revision, so individual figures cannot be re-checked against a specific revision. The citation markers in the text point to references that were not included in the capture.

## Related

- [[Email Security]]
- [[Botnet]]
- [[Phishing]]
- [[Firewall]]
- [[Threat Intelligence]]
- [[Cybercriminal]]
- [[Defences MOC]]
