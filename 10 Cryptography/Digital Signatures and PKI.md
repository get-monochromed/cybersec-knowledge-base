---
title: Digital Signatures and PKI
aliases: [PKI, Public Key Infrastructure, X.509, Digital Signature, Certificate]
category: crypto
tags: [crypto/pki, exam]
status: solid
up: "[[Cryptography MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Digital Signatures and PKI

## Summary

Signatures prove *who* created data and that it was not altered. PKI is the trust system that binds public keys to identities so those signatures (and TLS) mean something.

## Digital signatures

- Sign: `signature = Sign(private_key, H(message))` (hash-then-sign).
- Verify: `Verify(public_key, H(message), signature)`.
- Properties: **authenticity**, **integrity**, **non-repudiation** (the signer cannot credibly deny it, assuming the key was protected).
- Algorithms: Ed25519 (preferred, modern), ECDSA (P-256), RSA-PSS. Never raw RSA.
- Failure mode: **verification implemented incorrectly** (accepting `alg: none`, ignoring expiry, not checking the chain) — a recurring JWT/library CVE class.

## PKI components

- **CA** (certificate authority) — issues certificates; root CAs are trusted via the OS/browser trust store.
- **Intermediate CA** — signs end-entity certs; compromise is still catastrophic but revocable.
- **Registration authority** — identity vetting.
- **Certificate** (X.509) — binds public key to subject (CN/SAN), issuer, validity, key usage, extensions.
- **CSR** — certificate signing request.
- **Revocation** — CRL and OCSP; short-lived certificates are increasingly preferred to revocation.
- **Certificate Transparency** — public append-only logs of issued certs; enables detection of mis-issuance.

## Chain of trust

End-entity cert → intermediate(s) → root. Validation checks signature chain, validity dates, name match, key usage, revocation, and policy constraints. Any weak link (an intermediate that can issue for any domain) undermines everything.

## Where it matters

- **TLS** server and client certificates ([[TLS]]).
- **Code signing** — ensures software integrity; bypassed by stolen certs (supply-chain attacks).
- **Email** — S/MIME, DKIM ([[Email Security]]).
- **Document signing**, VPN authentication, 802.1X EAP-TLS, mTLS for service identity.
- **SSH** uses its own key model, but the same trust questions apply.

## Common failures

- Private key compromise or weak key generation (Debian OpenSSL bug).
- Mis-issued certificates; lookalike domains in CT logs.
- Clients that ignore validation errors (users clicking through warnings).
- Overly broad intermediate CAs and enterprise MITM roots ([[Man-in-the-Middle (MITM)]]).
- **Quantum**: RSA/ECDSA signatures will need migration ([[Post-Quantum Cryptography]]).

## Related

- [[Hashing]]
- [[Asymmetric Encryption]]
- [[TLS]]
- [[Key Management]]
- [[Cryptography MOC]]
