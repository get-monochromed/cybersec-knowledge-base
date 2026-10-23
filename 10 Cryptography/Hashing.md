---
title: Hashing
aliases: [Hash Function, Cryptographic Hash, Hash]
category: crypto
tags: [crypto/hash, exam]
status: solid
up: "[[Cryptography MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Hashing

## Summary

A one-way function mapping any input to a fixed-size digest. Used for integrity, password storage, digital signatures, and data structures. It provides **no confidentiality** — anyone can hash data.

## Properties

- **Pre-image resistance** — given a hash, cannot find the input.
- **Second pre-image resistance** — given an input, cannot find a different input with the same hash.
- **Collision resistance** — cannot find *any* two inputs with the same hash.
- **Avalanche effect** — one bit changed → completely different digest.
- **Deterministic** and fast to compute.

## Algorithms

| Algorithm | Output | Status |
|---|---|---|
| MD5 | 128-bit | broken — collisions trivial |
| SHA-1 | 160-bit | broken — collisions demonstrated (SHAttered) |
| SHA-256/512 (SHA-2) | 256/512 | secure, ubiquitous |
| SHA-3 (Keccak) | variable | secure, different construction |
| BLAKE2/BLAKE3 | variable | secure, very fast |

## Password storage

Fast hashes are the wrong tool for passwords: an attacker with a GPU tests billions of guesses per second.

- **Use a slow KDF**: **Argon2id** (preferred), scrypt, bcrypt, PBKDF2 (if FIPS). Memory-hard is the point.
- **Salt** each password with a unique random value — kills rainbow tables and cross-user comparison.
- **(Optional) pepper** — a secret appended and stored outside the database.
- Never encrypt passwords reversibly, never store unsalted MD5/SHA-1, and never use fast hashes regardless of iteration count alone.

## Integrity and MACs

- File integrity: `sha256sum`, checksums published over a trusted channel.
- **HMAC** — a keyed hash providing integrity + authenticity (HMAC-SHA256).
- **AEAD** modes (GCM) use a hash-like MAC internally.
- **Length-extension attacks** — SHA-2 Merkle–Damgård construction is vulnerable if you use `H(secret || message)`; use HMAC instead.

## Other uses

Content addressing (Git objects), Merkle trees (blockchain, certificate transparency, backups), deduplication, bloom filters, signatures (hash-then-sign).

## Related

- [[Symmetric Encryption]]
- [[Digital Signatures and PKI]]
- [[Password Attacks]]
- [[Cryptography]]
- [[Cryptography MOC]]
