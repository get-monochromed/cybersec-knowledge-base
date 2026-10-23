---
title: TLS
aliases: [TLS, SSL, HTTPS, Transport Layer Security, TLS 1.3]
category: crypto
tags: [crypto/protocol, network, exam]
status: solid
up: "[[Cryptography MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: ["RFC 8446 (TLS 1.3)"]
---

# TLS

## Summary

The protocol securing almost all internet traffic: confidentiality, integrity and authentication of endpoints. "SSL" is the obsolete predecessor; the version that matters is TLS 1.3 (2018), with 1.2 still acceptable when configured correctly.

## What TLS provides

- **Confidentiality** — symmetric encryption of the connection.
- **Integrity** — AEAD (GCM or ChaCha20-Poly1305).
- **Authentication** — server certificate validated against a trust store; optional client certificates (mTLS).
- **Forward secrecy** — ephemeral ECDHE keys mean a later private-key compromise does not decrypt recorded traffic.

## TLS 1.3 handshake (simplified)

1. ClientHello: supported versions, cipher suites, **key share** (X25519), SNI.
2. ServerHello: chosen suite, its key share; certificate + CertificateVerify (signed with the server key).
3. Both derive the same shared secret (ECDHE) → handshake keys → Finished.
4. Application data encrypted with derived keys.

**1-RTT** (vs 2-RTT in 1.2), and **0-RTT** resumption sends data immediately — but 0-RTT is **replayable**, so it must not be used for non-idempotent requests.

## Configuration

- TLS 1.3 + TLS 1.2 only; disable 1.0/1.1 and all SSL versions.
- Strong suites: `TLS_AES_128_GCM_SHA256`, `TLS_AES_256_GCM_SHA384`, `TLS_CHACHA20_POLY1305_SHA256` (1.3); ECDHE + AEAD for 1.2.
- Disable RSA key exchange (no forward secrecy), CBC-mode suites, RC4, 3DES, and export/null ciphers.
- Certificates: correct SANs, full chain, valid dates, automated renewal (ACME), strong keys (RSA 2048+/ECDSA P-256+).
- **HSTS** with `includeSubDomains` and preload (defeats SSL stripping).
- **OCSP stapling**; consider short-lived certs over CRL/OCSP complexity.
- **CAA** records restrict who may issue for your domain.

## Attacks and failure modes

- **Downgrade** — stripped by TLS 1.3's version negotiation and HSTS ([[Man-in-the-Middle (MITM)]]).
- **Certificate validation bypass** — the biggest practical issue: mobile apps with pinning disabled, users clicking through warnings, custom trust stores.
- **Weak or misconfigured servers** — expired certs, missing intermediates, shared keys.
- **TLS interception appliances** — break forward secrecy and create a single point of compromise.
- **Metadata leaks** — SNI, certificate names, traffic volume/timing remain visible; ECH (Encrypted Client Hello) is emerging.
- **Side channels** — compression (CRIME/BREACH), timing; avoid compression of secrets alongside attacker input.

## Testing

`testssl.sh`, `sslyze`, `nmap --script ssl-enum-ciphers`, SSL Labs. Certificate transparency monitoring for your domains.

## Related

- [[Digital Signatures and PKI]]
- [[Key Management]]
- [[Network Security]]
- [[Web Application Security]]
- [[Cryptography MOC]]
