---
title: Key Management
aliases: [KMS, Key Rotation, Secrets Management, HSM]
category: crypto
tags: [crypto/keys, operations]
status: solid
up: "[[Cryptography MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Key Management

## Summary

Generating, storing, distributing, rotating, and destroying keys. Cryptography fails here far more often than in the maths — a perfect cipher with a key in a Git repo is no protection. NIST SP 800-57 is the reference lifecycle.

## Lifecycle

1. **Generate** — in a CSPRNG-backed system, ideally inside an HSM/KMS.
2. **Distribute** — envelope encryption: data keys encrypted by a master/key-encryption key that never leaves the KMS.
3. **Store** — HSM, cloud KMS, secrets manager, OS keychain; never in code, config, or images.
4. **Use** — access-controlled, audited, least privilege; the key is used, not exported, where possible.
5. **Rotate** — on schedule and on suspected compromise; rotate data keys without re-encrypting everything by rotating the KEK.
6. **Revoke/destroy** — crypto-shredding is the reliable way to make data unrecoverable.

## Storage options

- **HSM** — tamper-resistant hardware, FIPS 140-2/3; the standard for CA keys, payment keys.
- **Cloud KMS** — managed HSM-backed keys with IAM and audit.
- **Secrets manager** — Vault, AWS Secrets Manager, SOPS+age for file-based secrets.
- **OS keychain / TPM** — for device-bound keys.
- **Never**: environment variables in CI logs, `.env` in repos, hard-coded in source, plaintext in backups.

## Envelope encryption

Encrypt data with a **DEK** (data encryption key); encrypt the DEK with a **KEK** held in the KMS. Rotating the KEK is cheap; access to the KEK is the real control. This is how cloud disk/storage encryption works.

## Secrets hygiene

- Scan repos and CI logs for secrets (gitleaks, trufflehog); rotate anything found, then remove from history.
- Short-lived credentials (OIDC federation) instead of long-lived cloud keys.
- Per-environment, per-service secrets; no shared keys across tenants.
- Break-glass procedure documented and tested.

## Common failures

- One key reused everywhere; no rotation for years.
- Backups encrypted with a key stored inside the same backup system.
- Developer laptops holding production keys.
- "Encrypted" data whose keys are in the same IAM boundary as the data (ransomware encrypts both).
- Losing the key = losing the data; Escrow and recovery must be designed, not improvised.

## Related

- [[Symmetric Encryption]]
- [[Asymmetric Encryption]]
- [[Digital Signatures and PKI]]
- [[TLS]]
- [[Cloud Security]]
- [[Cryptography MOC]]
