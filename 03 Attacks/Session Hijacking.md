---
title: Session Hijacking
aliases: [Session Theft, Cookie Theft, Token Theft, Session Fixation]
category: attack
tags: [attack/web, identity]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Session Hijacking

## Summary

Stealing or taking over an authenticated session so the attacker becomes the victim without knowing their password. Modern variants target the *token*, not the password — which is why MFA alone does not stop it.

## Techniques

- **Cookie/session token theft** — via [[Cross-Site Scripting]] (if not `HttpOnly`), malware, or a compromised browser extension.
- **Adversary-in-the-middle (AiTM) phishing** — reverse proxy (Evilginx) captures the session cookie *after* MFA succeeds. The single most important modern variant.
- **Session fixation** — attacker sets a known session ID (via URL parameter or a subdomain cookie) and waits for the victim to log in.
- **Session prediction** — weak/sequential session IDs (rare today, still seen in custom code).
- **Sidejacking** — sniffing cookies on plaintext HTTP or open Wi-Fi ([[Wireless Attacks]], [[Man-in-the-Middle (MITM)]]).
- **Token leakage** — tokens in URLs (referer leakage, logs), in localStorage (XSS-readable), in mobile app backups.
- **Pass-the-cookie / token replay** — using a stolen token from another device or country.

## Detection

- **Impossible travel**, new device/browser/ASN mid-session, IP change with no re-auth.
- Concurrent sessions from distant locations; user-agent changes.
- Session token used from two ASNs in short succession (classic replay signature).
- Login events with no corresponding MFA event (AiTM proxying).
- For Microsoft/Google: "session cookie theft" detections, token protection alerts, anomalous token issuance.

## Mitigation

- **`HttpOnly` + `Secure` + `SameSite`** on session cookies — blocks XSS theft and cross-site sending.
- **Short session lifetimes** and **re-authentication** for sensitive actions; idle + absolute timeouts.
- **Session rotation** on login and privilege change (defeats fixation).
- **Bind sessions** to device/client fingerprint where practical (token binding, DPoP, certificate-bound tokens).
- **Phishing-resistant MFA (FIDO2)** — origin-bound credentials are not replayable by a proxy. The real fix for AiTM.
- **Token protection / conditional access** — require compliant device, block token replay (`Continuous Access Evaluation`).
- **Revocation**: on any suspicion, invalidate all sessions server-side, not just the one device.
- **Never put tokens in URLs**; prefer `Secure` cookies over `localStorage`; keep the token lifetime short with refresh rotation.

## Related

- [[Cross-Site Scripting]]
- [[Phishing]]
- [[Man-in-the-Middle (MITM)]]
- [[Authentication, Authorization and Accounting]]
- [[Attacks MOC]]
