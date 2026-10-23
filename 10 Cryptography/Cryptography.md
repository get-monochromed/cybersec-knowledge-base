---
title: Cryptography
aliases: [Crypto Basics, Cryptographic Primitives]
category: crypto
tags: [crypto/overview, exam]
status: solid
up: "[[Cryptography MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Cryptography

## Summary

Cryptography provides four things: **confidentiality** (encryption), **integrity** (hashing/MACs), **authenticity** (signatures, MACs), and **non-repudiation** (digital signatures). Nearly every security control above the network layer depends on it working correctly.

## The primitives

| Goal | Primitive | Examples |
|---|---|---|
| Confidentiality | symmetric encryption | AES-GCM, ChaCha20-Poly1305 |
| Key exchange | asymmetric / DH | ECDHE (X25519), RSA-KEM |
| Integrity | hash | SHA-256, SHA-3, BLAKE3 |
| Integrity + authenticity (shared key) | MAC | HMAC-SHA256, Poly1305 |
| Authenticity + non-repudiation | digital signature | Ed25519, ECDSA, RSA-PSS |
| Password storage | slow KDF | Argon2id, scrypt, bcrypt, PBKDF2 |
| Randomness | CSPRNG | `getrandom`, `/dev/urandom` |

## Symmetric vs asymmetric

Symmetric is fast but needs a shared secret; asymmetric solves key distribution but is slow. Real systems **hybridise**: asymmetric (or ECDHE) to agree a key, symmetric to encrypt the data. That is exactly what [[TLS]] does.

## Classical → modern

Caesar/substitution/Vigenère are historically interesting and trivially broken by frequency analysis ([[Cryptanalysis]]). The Enigma failure mode — operational mistakes, not mathematics — is a recurring theme in real breaches (nonce reuse, key reuse, weak randomness).

## What actually goes wrong in practice

Not broken algorithms, but:

- **Misuse**: ECB mode, static IVs, nonce reuse in GCM (catastrophic — leaks the authentication key).
- **Bad randomness** — predictable keys/IVs.
- **Missing authentication** — encryption without integrity (padding oracles, bit-flipping).
- **Key management** — keys in code, in repos, unrotated, shared.
- **Protocol design** — custom schemes, downgrade paths, missing binding of identity to key.
- **Implementation bugs** — padding oracles, timing leaks, side channels.

## Related

- [[Symmetric Encryption]]
- [[Asymmetric Encryption]]
- [[Hashing]]
- [[Digital Signatures and PKI]]
- [[Key Management]]
- [[Cryptography MOC]]
