---
title: Peer List Poisoning
aliases: [Peerlist Poisoning, P2P Botnet Poisoning]
category: defensive
tags: [defensive/disruption, botnet]
status: developing
up: "[[Defensive Ops MOC]]"
created: 2026-10-24
updated: 2026-10-24
sources: ["[[_Archive/2026-10-24-zombie-spider-kelihos]]"]
---

# Peer List Poisoning

## Summary

A botnet disruption technique used against peer-to-peer (P2P) designs. Instead of seizing servers, the operation injects a crafted peer list into the botnet so that infected machines only accept peers controlled by the defenders — cutting the operator off from his own network and steering it into a sinkhole. It was the mechanism used against [[Kelihos]] in April 2017.

## How it works

1. The botnet's peer list is the set of addresses a bot uses to find the rest of the network.
2. The operation crafts a peer list containing only infrastructure it controls.
3. That list is propagated through the network until bots adopt it as their source of truth for peers.
4. The operator can no longer reach the bots, and the bots can no longer reach the operator's backend.

The end state is a **topology change**: a decentralised mesh becomes a star, with the sinkhole at the centre. Bots keep running and keep checking in, but every check-in goes to law enforcement.

## Why it works

- P2P exists to remove the single point of failure that a central C2 server represents; peer discovery is therefore the part of the design that *must* be reachable and mutable.
- The technique turns the botnet's own resilience against it: the mechanism that lets it survive takedown is the mechanism that lets a takedown be propagated.
- It avoids the two usual costs of disruption — no need to sink or seize the criminal's servers, and no need to disinfect victims first.

## Preconditions and limits

- Requires reverse engineering of the peer-list protocol and the ability to sign or forge entries the bots will accept (Kelihos used layered crypto including RSA and Blowfish to resist exactly this).
- Requires enough propagation to reach critical mass before the operator notices and rotates keys.
- **It does not remove the malware.** Infected hosts remain infected and must be remediated locally; the sinkhole turns them into a census, not a cleanup.
- It buys time, not permanence: rebuilt generations or rotated peer lists recover (Kelihos itself was rebuilt after earlier takedowns).

> [!warning] Unverified
> The source describes the outcome ("the P2P network was transformed into a centralized network, with infected systems only allowed to communicate with a sinkhole") but not the injection mechanics, key handling or how the list was accepted. The steps above are a general reading of peer-list poisoning, not details confirmed by this clipping.

## Related

- [[Kelihos]]
- [[Botnet]]
- [[Threat Hunting]]
- [[Incident Response]]
- [[Defensive Ops MOC]]
