---
title: Password Attacks
aliases: [Credential Attacks, Brute Force, Credential Stuffing, Password Spraying]
category: attack
tags: [attack/credential, identity, exam]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Password Attacks

## Summary

Obtaining or guessing credentials. The cheapest route into almost any environment — no exploit, no malware, just a valid login. MITRE groups these under credential access (T1110).

## Techniques

| Technique | Mechanism | Noise | Countered by |
|---|---|---|---|
| **Brute force** | try every combination | very high | lockout, rate limit, length |
| **Dictionary attack** | wordlist of common/leaked passwords | high | blocklist leaked passwords, length |
| **Credential stuffing** | replay username/password pairs from other breaches | medium | MFA, breached-password checks, device binding |
| **Password spraying** | few common passwords × many accounts (e.g. `Summer2026!`) | low | smart lockout, banned-password list |
| **Hybrid / rule-based** | dictionary + mutations (`P@ssw0rd123`) | high | length over complexity |
| **Offline cracking** | dump hashes, crack locally | requires access first | slow hashes (Argon2/bcrypt), long random passwords |
| **Password interception** | phishing, [[Man-in-the-Middle (MITM)]], keylogger ([[Spyware and Keyloggers]]) | low | phishing-resistant MFA, TLS |
| **Default credentials** | vendor defaults never changed | low | hardening baseline, [[Attack Surface]] reduction |
| **Kerberoasting / AS-REP roasting** | request service tickets, crack offline | low | strong service account passwords, gMSA |

## Spraying vs brute force

Brute force targets one account hard and trips lockout. Spraying does one guess against every account, stays under lockout thresholds, and is why "3 attempts then lock" is not enough — you need [[SIEM]] detection on distributed failure patterns and a banned-password list.

## Offline cracking reality

Modern GPUs/rigs test billions of guesses per second against fast hashes (MD5/SHA-1). Mitigations: memory-hard hashes (Argon2id, scrypt, bcrypt), salting (kills rainbow tables), pepper, high cost factors. Password *length* and randomness dominate: `correct horse battery staple` beats `P@ssw0rd`.

## Detection

- Spike in failed logins per account or per source IP; failure followed by success ("one success after 50 failures").
- Distributed low-and-slow failures across many accounts from few IPs, or many IPs against one account.
- Login from new ASN/country, legacy auth protocols, unusual user agents.
- Identity provider alerts: risky sign-in, password spray detection, leaked-credential match.

## Mitigation

- **MFA** — phishing-resistant (FIDO2) where possible; TOTP is bypassable by AiTM phishing.
- **Banned/breached password screening** and minimum length (12–16+), drop forced rotation (it produces `Password1!` → `Password2!`).
- **Rate limiting / smart lockout** and progressive delays.
- **Slow hashing** at rest (see [[Hashing]]); never plaintext or reversible encryption.
- **Privileged access management**, unique passwords per account (password manager), no sharing.
- **Detection**: [[SIEM]] rules on spray patterns; alert on legacy auth.

## Related

- [[Phishing]]
- credential access (see [[Post Exploitation]])
- [[Authentication, Authorization and Accounting]]
- [[Hashing]]
- [[Attacks MOC]]
