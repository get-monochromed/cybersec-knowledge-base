---
title: Asymmetric Encryption
aliases: [Public Key Cryptography, RSA, ECC, Diffie-Hellman]
category: crypto
tags: [crypto/asymmetric, exam]
status: solid
up: "[[Cryptography MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Asymmetric Encryption

## Summary

Two mathematically linked keys: what one encrypts, only the other decrypts. Solves key distribution — publish the public key, keep the private one. Slow, so it is used for key exchange and signatures rather than bulk data.

## Key pairs

- **Public key** — share freely; used to encrypt *to* the owner or verify their signature.
- **Private key** — never leaves the owner; used to decrypt or sign.

## Algorithms

- **RSA** — security from integer factorisation. 2048-bit minimum today, 3072+ preferred; 1024 is dead. Encryption (OAEP padding only) and signatures (PSS).
- **ECC** — security from discrete logarithms on elliptic curves; much smaller keys for equivalent strength. P-256 (ECDSA/ECDH), Curve25519 (X25519 for key exchange, Ed25519 for signatures).
- **Diffie-Hellman** — key agreement, not encryption; **ECDHE** gives forward secrecy. Classic DH with weak parameters is a common finding.
- **ElGamal** — historical/theoretical.

## What they are actually used for

1. **Key exchange** — agree a symmetric session key (TLS ECDHE). Ephemeral keys → forward secrecy: compromising the long-term key later does not decrypt past sessions.
2. **Digital signatures** — authenticate origin and integrity ([[Digital Signatures and PKI]]).
3. **Key transport** — encrypt a symmetric key (RSA-KEM), used in some protocols.

## Failure modes

- **Padding oracles** (RSA PKCS#1 v1.5) — Bleichenbacher attacks; fixed by OAEP and constant-time handling.
- **Weak parameters** — small keys, non-safe-prime DH groups, insufficient entropy.
- **Key substitution / MITM** — the public key must be bound to an identity, which is [[Digital Signatures and PKI|PKI]]'s job.
- **Reusing keys across purposes** — signing with an encryption key, or vice versa.
- **Quantum** — Shor's algorithm breaks RSA/ECC entirely ([[Post-Quantum Cryptography]]).

## Related

- [[Symmetric Encryption]]
- [[Digital Signatures and PKI]]
- [[Key Management]]
- [[TLS]]
- [[Cryptography MOC]]
