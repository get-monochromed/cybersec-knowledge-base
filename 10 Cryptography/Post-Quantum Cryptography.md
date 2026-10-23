---
title: Post-Quantum Cryptography
aliases: [PQC, Quantum-Resistant Crypto, ML-KEM, ML-DSA, Harvest Now Decrypt Later]
category: crypto
tags: [crypto/pqc, emerging]
status: solid
up: "[[Cryptography MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: ["NIST FIPS 203/204/205 (2024)"]
---

# Post-Quantum Cryptography

## Summary

Algorithms designed to resist attacks by quantum computers. Not a future problem: traffic captured today can be decrypted later once a cryptographically relevant quantum computer exists ("harvest now, decrypt later"), so migration has already started.

## Why

- **Shor's algorithm** breaks RSA, ECC, Diffie–Hellman completely — all key exchange and signatures on the internet.
- **Grover's algorithm** gives a quadratic speedup on symmetric search: AES-128 → ~64-bit effective, AES-256 → ~128-bit effective (still safe).

## NIST standards (2024)

| Standard | Algorithm | Purpose |
|---|---|---|
| **FIPS 203** | ML-KEM (CRYSTALS-Kyber) | key encapsulation (replaces ECDHE/RSA-KEM) |
| **FIPS 204** | ML-DSA (CRYSTALS-Dilithium) | digital signatures |
| **FIPS 205** | SLH-DSA (SPHINCS+) | hash-based signatures (conservative fallback) |
| Backup KEM | HQC | selected as an alternative to ML-KEM |

Status: standardised, implementations maturing; not yet a drop-in for everything (larger keys/signatures, performance, protocol changes).

## Migration reality

- **Hybrid mode first**: combine classical + PQC (e.g. `X25519MLKEM768`) so security holds if either is broken. Browsers and major CDNs already default to hybrid key exchange.
- **Signatures are the harder half** — certificates, code signing, firmware, long-lived documents. Larger signatures break size assumptions in protocols.
- **Inventory cryptography**: you cannot migrate what you cannot find (crypto-agility, CBOM).
- **Prioritise long-lived confidentiality** (backups, health records, state secrets) — those are the harvest-now targets.
- Firmware/embedded devices with 20-year lifetimes need planning now.

## Practical actions

1. Crypto inventory + crypto-agility in design (algorithm identifiers negotiated, not hard-coded).
2. Enable hybrid TLS key exchange where supported.
3. Test PQC libraries (liboqs, OpenSSL 3.5+, BoringSSL) in non-production.
4. Track NIST/NSA CNSA 2.0 timelines and vendor roadmaps.
5. Do not invent your own — the parameter sets and implementation pitfalls are unforgiving.

## Related

- [[Asymmetric Encryption]]
- [[Key Management]]
- [[TLS]]
- [[Digital Signatures and PKI]]
- [[Cryptography MOC]]
