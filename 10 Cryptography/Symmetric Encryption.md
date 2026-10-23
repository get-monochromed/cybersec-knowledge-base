---
title: Symmetric Encryption
aliases: [AES, Shared-Key Encryption, Block Cipher, Stream Cipher]
category: crypto
tags: [crypto/symmetric, exam]
status: solid
up: "[[Cryptography MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Symmetric Encryption

## Summary

One key encrypts and decrypts. Fast enough for bulk data (disk, TLS records, backups), which is why every real protocol uses it for the payload. The hard problem is distributing and protecting the key ([[Key Management]]).

## Algorithms

- **AES** — 128/192/256-bit block cipher, hardware-accelerated (AES-NI). The default.
- **ChaCha20** — stream cipher; faster than AES without hardware support (mobile, embedded).
- **3DES** — legacy, deprecated (Sweet32).
- **DES** — broken (56-bit).

## Modes of operation

| Mode | Property | Use |
|---|---|---|
| **ECB** | identical plaintext → identical ciphertext | **never** (leaks structure) |
| **CBC** | needs random IV, padding, no integrity | legacy; padding-oracle prone |
| **CTR** | stream-like, needs unique nonce | building block |
| **GCM** | AEAD: encryption + authentication | default choice (AES-GCM) |
| **CCM** | AEAD for constrained devices | IoT |
| **XTS** | disk encryption mode | full-disk encryption |

**AEAD** (Authenticated Encryption with Associated Data) is the requirement: GCM or ChaCha20-Poly1305. Never CBC without a MAC, and never a homemade encrypt-then-MAC.

## Nonce/IV rules

- GCM: a nonce must **never repeat** under the same key. Repetition leaks the authentication key and allows forgery — this has caused real CVEs (e.g. in VPN and Wi-Fi implementations).
- CTR: same uniqueness requirement.
- CBC: unpredictability (random) is required, not just uniqueness.

## Key sizes

AES-128 is fine for most purposes; AES-256 for compliance/post-quantum margin (Grover halves effective strength to 128 bits, still safe). Larger keys do not fix bad modes or bad key management.

## Performance

AES-GCM runs at GB/s with AES-NI; ChaCha20-Poly1305 is competitive in software. Disk encryption: LUKS/dm-crypt (AES-XTS), BitLocker, FileVault.

## Related

- [[Asymmetric Encryption]]
- [[Hashing]]
- [[Key Management]]
- [[Cryptography]]
- [[Cryptography MOC]]
