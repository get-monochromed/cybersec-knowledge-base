---
title: Supply Chain Attack
aliases: [Software Supply Chain Attack, Third-Party Risk, Dependency Attack]
category: attack
tags: [attack/supply-chain, owasp-a08]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Supply Chain Attack

## Summary

Compromise not the target but something the target trusts: a library, a vendor, an update channel, a build pipeline, or an MSP. Extremely efficient — one compromise reaches thousands of victims, with the victim's own trust relationship doing the delivery.

## Where it strikes

- **Dependencies** — malicious package versions (typosquatting, dependency confusion, hijacked maintainer accounts), e.g. event-stream, ua-parser-js, the xz-utils backdoor.
- **Build systems / CI-CD** — compromised runners, leaked deployment tokens, poisoned build artifacts (SolarWinds Orion).
- **Update channels** — legitimate updater delivering malicious payload (NotPetya via M.E.Doc, CCleaner).
- **Managed service providers** — one RMM compromise gives access to all clients (Kaseya, ConnectWise).
- **Hardware/firmware** — implants, backdoored appliances, counterfeit network gear.
- **Open-source maintainer social engineering** — long-game trust building then malicious commit.
- **Vendor remote access** — third-party support accounts into your network.

## Why it is hard

- The malicious code arrives **signed** and via an expected channel, so signature and reputation checks pass.
- Detection requires knowing what *should* be in your build, which most organisations cannot enumerate.
- Trust is transitive but accountability is not.

## Detection

- **SBOM** (CycloneDX/SPDX) and dependency diffing — alert on new transitive dependencies and version jumps.
- Anomalous process behaviour from trusted software (SolarWinds' implant ran inside a signed DLL): EDR behavioural rules, not signatures.
- CI/CD telemetry: new workflow steps, unexpected outbound connections from build runners, secrets accessed by unusual jobs.
- Egress anomalies from servers that should never talk to the internet.
- Vulnerability intel on your exact dependency graph ([[Vulnerability Management]]).

## Mitigation

- **Pin and verify**: lockfiles, hash pinning, signed artifacts (Sigstore/cosign), private registries with allow-lists.
- **SBOM** generation and consumption; know your transitive tree.
- **Build hardening**: SLSA-style provenance, isolated ephemeral runners, least-privilege CI tokens, no long-lived cloud keys.
- **Dependency review** before adoption: maintainer count, age, activity, install scripts.
- **Vendor risk management**: security questionnaires, contractual breach notification, least-privilege vendor access, no standing VPN.
- **Egress filtering and segmentation** — assume one dependency will be compromised.
- **Rapid patch capability** for the "everyone patch now" moments.

## Related

- [[Vulnerability Management]]
- [[Container Security]]
- [[Application Security]]
- [[Advanced Persistent Threat]]
- [[Attacks MOC]]
