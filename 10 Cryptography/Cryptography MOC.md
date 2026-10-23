---
title: Cryptography MOC
aliases: [Crypto, Applied Cryptography]
category: index
tags: [moc]
status: solid
up: "[[Home]]"
created: 2026-10-23
updated: 2026-10-23
---

# Cryptography

The mathematics that makes confidentiality, integrity and authentication possible — and the practical failures that make it useless (bad randomness, reused nonces, homemade protocols).

## Primitives

- [[Symmetric Encryption]] — AES, ChaCha20; fast, shared key
- [[Asymmetric Encryption]] — RSA, ECC; key exchange and signatures
- [[Hashing]] — integrity, password storage, MACs
- [[Digital Signatures and PKI]] — identity binding, certificates
- [[Cryptanalysis]] — how it breaks
- [[Key Management]] — where most real failures live

## Protocols and systems

- [[TLS]] — everything on the web
- [[Passkeys]] — phishing-resistant authentication
- [[Post-Quantum Cryptography]] — the migration already underway

## Rules that never change

1. **Never invent your own crypto or protocol.** Use vetted libraries and standard constructions.
2. **Kerckhoffs's principle** — security must rest on the key, not on secrecy of the algorithm.
3. **Encrypt-then-MAC / AEAD**, never custom composition.
4. **Randomness is the foundation** — use a CSPRNG (`/dev/urandom`, `getrandom`); never `rand()` for keys or nonces.
5. **Key management outlives the algorithm choice.** Rotation, storage, and access control decide whether crypto helps.

## Related

- [[Foundations MOC]]
- [[TLS]] · [[VPN]] · [[Digital Signatures and PKI]]
