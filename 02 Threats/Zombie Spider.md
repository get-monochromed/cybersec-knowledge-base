---
title: Zombie Spider
aliases: [ZOMBIE SPIDER, Pyotr Levashov, Peter Severa]
category: actor
tags: [actor/financial, botnet]
status: stub
up: "[[Threats MOC]]"
created: 2026-10-24
updated: 2026-10-24
sources: ["[[_Archive/2026-10-24-zombie-spider-kelihos]]"]
---

# Zombie Spider

## Summary

CrowdStrike's designation for the criminal operator behind the [[Kelihos]] botnet and its predecessors **Waledac** and **Storm**. Publicly identified as **Pyotr Levashov**, also known as **Peter Severa**; arrested in April 2017 in an FBI-led international operation, the same operation that dismantled Kelihos. The identity is public record via the US Department of Justice announcement cited by the source.

## Motivation

Financial. Ran the botnet as a service — selling spam, banking-Trojan, ransomware and DDoS delivery to other criminals — rather than using it for a single campaign.

## Capability

- Sustained operation of a large P2P botnet across three generations (Storm → Waledac → Kelihos), rebuilding after each takedown.
- Multi-purpose plugin architecture: spam, credential and email harvesting, DDoS, click fraud, fast-flux DNS hosting.
- Deliberate anti-analysis engineering: layered encryption (RSA, Blowfish) and custom protocol obfuscation.
- Criminal-as-a-service business model, anticipating the RaaS/affiliate pattern now standard among [[Cybercriminal]] actors.

## Typical TTPs

- Bulk spam delivery and illegal pharmaceutical advertising.
- Distribution of banking Trojans and remote access tools to harvested victims.
- Ransomware deployment through the botnet.
- DDoS-for-hire, click fraud, and pump-and-dump stock promotion.
- Fast-flux DNS to keep infrastructure alive.

## Defensive focus

- Treat infected hosts, not just blocked domains, as the unit of response: takedown left victims infected (see [[Peer List Poisoning]]).
- Egress filtering for P2P peer discovery, sinkhole traffic monitoring, mail filtering for spam campaigns.
- Attribution is not the control: the same infrastructure pattern is available to any buyer of botnet capacity.

> [!warning] Unverified
> The source states the operator "won a spot on the top 10 list of the world's worst spammers maintained by Spamhaus" but gives no list name, date or reference. This is a 2017 vendor-blog claim about a historic ranking, not current [[Spamhaus Project]] data.
>
> The DOJ press release itself was not captured, so charges, jurisdiction and outcome are not recorded here — only that the arrest was announced in April 2017 as part of the operation against Kelihos.

## Related

- [[Kelihos]]
- [[Cybercriminal]]
- [[Threat Actor]]
- [[Spamhaus Project]]
- [[Threats MOC]]
