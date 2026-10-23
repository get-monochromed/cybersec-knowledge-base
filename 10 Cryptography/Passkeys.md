---
title: Passkeys
aliases: [Passkey, WebAuthn, FIDO2, Security Key]
category: crypto
tags: [crypto/auth, identity, phishing]
status: solid
up: "[[Cryptography MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: ["W3C WebAuthn Level 2/3", "FIDO2"]
---

# Passkeys

## Summary

Phishing-resistant credentials based on public-key cryptography, bound to a website's origin. The private key never leaves the authenticator; the server stores only the public key. The strongest generally-available defence against [[Phishing]] and [[Session Hijacking|session theft]].

## How it works

1. Registration: the authenticator generates a key pair per site; the site stores the public key.
2. Authentication: the site sends a random challenge; the authenticator signs it with the private key, after user verification (biometric/PIN).
3. The signature is bound to the **origin** (RP ID), so a lookalike domain cannot reuse it.

## FIDO2 stack

- **WebAuthn** — browser API.
- **CTAP2** — protocol between browser/OS and authenticator (USB/NFC/BLE, platform authenticator).
- **Authenticator types**: platform (Touch ID, Windows Hello, Android/iOS passkeys) vs roaming (YubiKey).
- **Discoverable credentials** ("passkeys" in the consumer sense) allow username-less login and are synced by the platform keychain (iCloud Keychain, Google Password Manager). **Device-bound** keys are not synced — better for high assurance.
- **Attestation** — optional proof of authenticator make/model; privacy trade-offs.

## Why it beats TOTP/push

- No shared secret to phish; an AiTM proxy cannot replay the signature because the origin differs.
- No OTP codes to relay or fatigue-approve.
- Resistant to credential stuffing (no password exists).

## Deployment considerations

- **Account recovery** is the new weak point: if recovery falls back to SMS/email, the attacker targets that instead. Harden recovery flows.
- **Synced passkeys** trade some assurance for usability; require device-bound/hardware keys for admins and high-value accounts.
- **Cross-platform** support is now good but not universal; keep a fallback (TOTP) with monitoring, or hardware keys for staff.
- **Legacy systems** (VPN appliances, older SSO) may not support WebAuthn — that is a procurement criterion.
- **Inventory** credentials: users with a passkey should not retain a password+MFA path that bypasses it.

## Related

- [[Authentication, Authorization and Accounting]]
- [[Phishing]]
- [[Session Hijacking]]
- [[Digital Signatures and PKI]]
- [[Cryptography MOC]]
