---
title: Cryptanalysis
aliases: [Cryptanalysis, Cryptographic Attacks, Breaking Crypto]
category: crypto
tags: [crypto/attacks, exam]
status: solid
up: "[[Cryptography MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Cryptanalysis

## Summary

Attacking the cryptography rather than the implementation around it. In practice, almost no one breaks AES or RSA — they break *usage*: weak keys, reused nonces, bad randomness, missing authentication, and homemade protocols.

## Classic attacks

- **Brute force / exhaustive search** — infeasible against modern key sizes; relevant only for weak passwords and short keys.
- **Frequency analysis** — defeats substitution ciphers ([[Cryptography]] history).
- **Known-plaintext** — attacker has plaintext/ciphertext pairs; weakens simple ciphers, not AES.
- **Chosen-plaintext / chosen-ciphertext** — the attacker can query an encryption/decryption oracle; basis of padding-oracle attacks.
- **Meet-in-the-middle** — reduces double encryption to the cost of single (why 2DES ≈ DES security).

## Attacks that still work in the real world

| Attack | Target | Fix |
|---|---|---|
| **Padding oracle** | CBC mode + distinguishable errors | use AEAD (GCM), constant-time errors |
| **Bleichenbacher** | RSA PKCS#1 v1.5 | OAEP, constant-time |
| **Nonce reuse** | GCM/CTR | unique nonces, random 96-bit or counter |
| **Bit flipping** | CBC/CTR without MAC | AEAD |
| **Downgrade** | protocols negotiating versions | disable old versions, HSTS |
| **Birthday attack** | collision resistance (hash) | 256-bit hashes |
| **Length extension** | Merkle–Damgård hashes in naive MACs | HMAC |
| **Side channel** (timing, power, cache) | implementations | constant-time code, vetted libraries |
| **Weak randomness** | key/IV generation | CSPRNG |
| **Rainbow tables** | unsalted password hashes | salts + memory-hard KDFs |

## Quantum

**Shor's algorithm** breaks RSA/ECC/DH outright; **Grover's** halves symmetric key strength (AES-256 remains fine). See [[Post-Quantum Cryptography]].

## The practical lesson

Threat models rarely include "someone breaks AES". They include: a key in a repo, a reused IV in a VPN, a JWT with `alg: none`, an expired certificate, a homemade "encryption" that is base64, and a random number generator seeded with time. Audit usage, not mathematics.

## Related

- [[Symmetric Encryption]]
- [[Asymmetric Encryption]]
- [[Hashing]]
- [[Key Management]]
- [[Cryptography MOC]]
