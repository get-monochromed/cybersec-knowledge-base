---
title: 2026-10-24-spamhaus-project
aliases: [Spamhous Project clipping]
category: source
tags: [source/web-clip, email, reputation]
status: solid
up: "[[Reference MOC]]"
ingested: 2026-10-24
produced: ["[[Spamhaus Project]]"]
sources: []
---

> [!note] Ingest record
> Web clipping of the Wikipedia article on the Spamhaus Project. Produced [[Spamhaus Project]] (new note) plus glossary and acronym entries; no existing vault note was superseded.
>
> Provenance gap: no URL, retrieval date or article revision was captured, and the inline citation markers point at references that were not included. Figures that depend on them are flagged `Unverified` in the note rather than corrected.
>
> Ambiguities carried forward: ROKSO public availability ("after 2023") and ZEN's exact composition.

**The Spamhaus Project** is an international organisation based in [Andorra](https://en.wikipedia.org/wiki/Andorra "Andorra"), founded in 1998 by [Steve Linford](https://en.wikipedia.org/wiki/Steve_Linford "Steve Linford") to track [email spammers](https://en.wikipedia.org/wiki/Email_spam "Email spam") and [spam](https://en.wikipedia.org/wiki/Spam_\(electronic\) "Spam (electronic)")-related activity. The name _spamhaus_, a pseudo-[German](https://en.wikipedia.org/wiki/German_language "German language") expression, was coined by Linford to refer to an [Internet service provider](https://en.wikipedia.org/wiki/Internet_service_provider "Internet service provider") (ISP), or other firm, which spams or knowingly provides service to spammers.

## Anti-spam lists

The Spamhaus Project is responsible for compiling several widely[[2]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-2) used anti-spam lists. Many[[3]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-3) [Internet service providers](https://en.wikipedia.org/wiki/Internet_service_provider "Internet service provider") and [email servers](https://en.wikipedia.org/wiki/Email_server "Email server") use the lists to reduce the amount of spam that reaches their users. In 2006, the Spamhaus services protected 650 million email users, including the European Parliament, US Army, the White House and Microsoft, from billions of spam emails a day.[[4]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-guardian1-4)

Spamhaus distributes the lists in the form of DNS-based blocklists ([DNSBLs](https://en.wikipedia.org/wiki/DNSBL "DNSBL")). The lists are offered as a free public service to low-volume mail server operators on the internet.[[5]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-5) Commercial spam filtering services and other sites performing large scale usage must instead sign up for a commercial account through Spamhaus Technology its partner for distribution. Spamhaus outlines the way its DNSBL technology works in a document called "Understanding DNSBL Filtering."[[6]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-6)

The **Spamhaus Blocklist (SBL)**[[7]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-7) targets "verified spam sources (including spammers, spam gangs and spam support services)." Its goal is to list [IP addresses](https://en.wikipedia.org/wiki/IP_addresses "IP addresses") belonging to known spammers, spam operations, and spam-support services.[[8]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-8) The SBL's listings are partially based on the [ROKSO](https://en.wikipedia.org/wiki/The_Spamhaus_Project#Register_of_Known_Spam_Operations) index of known spammers.

The **Exploits Blocklist (XBL)** [[9]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-9) targets "illegal 3rd party exploits, including [open proxies](https://en.wikipedia.org/wiki/Open_proxy "Open proxy"), worms/viruses with built-in spam engines, virus-infected PCs & servers and other types of trojan-horse exploits." That is to say it is a list of known open proxies and exploited computers being used to send spam and viruses. The XBL includes information gathered by Spamhaus as well as by other contributing DNSBL operations such as the [Composite Blocking List](https://en.wikipedia.org/wiki/Composite_Blocking_List "Composite Blocking List") (CBL).

The **Policy Blocklist (PBL)**[[10]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-10) is similar to a [Dialup Users List](https://en.wikipedia.org/wiki/Dialup_Users_List "Dialup Users List"). It lists not only dynamic IP addresses but also static addresses that should not be sending email directly to third-party servers. Examples of such are an ISP's core routers, corporate users required by policy to send their email via company servers, and unassigned IP addresses. Much of the data is provided to Spamhaus by the organizations that control the IP address space, typically ISPs.

The **Domain Blocklist (DBL)**[[11]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-11) was released in March 2010 and is a list of domain names, which is both a domain [URI](https://en.wikipedia.org/wiki/Uniform_resource_identifier "Uniform resource identifier") blocklist and [RHSBL](https://en.wikipedia.org/wiki/DNSBL#URI_DNSBLs "DNSBL"). It lists spam domains including spam payload URLs, spam sources and senders ("right-hand side"), known spammers and spam gangs, and phish, virus and [malware](https://en.wikipedia.org/wiki/Malware "Malware")-related sites. It later added a zone of "abused URL shorteners", a common way spammers insert links into spam emails.

The **Combined Spam Sources (CSS)**[[12]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-12) is an automatically produced dataset of IP addresses that are involved in sending low-reputation email. Listings can be based on HELO greetings without an A record, generic looking rDNS or use of fake domains, which could indicate [spambots](https://en.wikipedia.org/wiki/Spambot "Spambot") or server misconfiguration. CSS is part of SBL.

The **ZEN Blocklist** [[13]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-13) is a combined list, which includes all the Spamhaus IP-based DNS Blocklists.

The **Botnet Controller List (BCL)**[[14]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-14) was released in June 2012 and is a list of IP addresses. It lists IP addresses of which Spamhaus personnel believe to be operated by cybercriminals for the exclusive purpose of hosting botnet Command&Control infrastructure. Such infrastructure is commonly used by cybercriminals to control malware infected computers.

The Spamhaus **DROP ("Don't Route Or Peer")** lists are JSON files delineating [CIDR blocks](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_blocks "Classless Inter-Domain Routing") and [ASNs](https://en.wikipedia.org/wiki/Autonomous_system_\(Internet\) "Autonomous system (Internet)") that have been stolen or are otherwise "totally controlled by spammers or 100% spam hosting operations".[[15]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-TiptonKrause2008-15)[[16]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-DROPLists-16) As a small subset of the SBL, it does not include address ranges registered to ISPs and sublet to spammers, but only those network blocks wholly used by spammers. It is intended to be incorporated in firewalls and routing equipment to drop all network traffic to and from the listed blocks.[[15]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-TiptonKrause2008-15) The DROP webpage FAQ[[17]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-17) states the data is free for all to download and use. In 2012 Spamhaus Technology offered a [BGP](https://en.wikipedia.org/wiki/BGP "BGP") feed of the same data.

The Spamhaus **Register of known spam operations (ROKSO)** is a database of spammers and spam operations who have been terminated from three or more ISPs due to spamming. It contains publicly sourced information about these persons and their domains, addresses and aliases.[[18]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-Jones2005-18)

ROKSO stopped being available to the public at some point after 2023.[[19]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-19)[[20]](https://en.wikipedia.org/wiki/The_Spamhaus_Project#cite_note-20) However, there is a special version available to [law enforcement](https://en.wikipedia.org/wiki/Law_enforcement "Law enforcement") agencies, containing data on hundreds of spam gangs, with evidence, logs and information on illegal activities of these gangs.