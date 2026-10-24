---
title: Cross-Site Scripting
aliases: [XSS, Cross Site Scripting]
category: attack
tags: [attack/web, owasp-a05, injection, exam]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Cross-Site Scripting

## Summary

Injecting JavaScript that executes in another user's browser in the context of the vulnerable site — so it can read that site's DOM, cookies (unless `HttpOnly`), and perform actions as the victim. It is an injection bug whose interpreter is the browser.

## Variants

- **Reflected** — payload travels in the request and is echoed in the response (search pages, error messages). Needs a crafted link.
- **Stored (persistent)** — payload saved server-side and served to every visitor (comments, profiles, support tickets). Worst impact, no interaction trick needed.
- **DOM-based** — client-side JavaScript copies attacker-controlled data into a sink (`innerHTML`, `document.write`, `eval`, `location`) without server involvement; the server may never see the payload.
- **Mutation XSS (mXSS)** — sanitised HTML re-parsed differently by the browser.
- **Self-XSS** — requires the victim to paste code; usually a social-engineering chain.

## Impact

Session theft ([[Session Hijacking]]), credential phishing rendered inside the real domain, keylogging, defacement, CSRF-token bypass (XSS defeats CSRF tokens), worm propagation in social apps, and full account takeover.

## Detection

- SAST: sources (`req.query`, `location.hash`) reaching sinks (`innerHTML`, `res.send` with HTML).
- DAST/fuzzing with context-aware payloads; CSP violation reports.
- Logs: `<script`, `onerror=`, `javascript:` in request parameters; unusual encoded payloads.
- Browser-side: CSP reports are the best production sensor.

## Mitigation

1. **Output encoding by context** — HTML, attribute, JS, CSS, URL each need different encoding. Encode at the sink, not the source.
2. **Framework defaults** — React/Vue/Angular escape by default; the bug appears via `dangerouslySetInnerHTML`, `v-html`, `bypassSecurityTrust*`.
3. **Avoid HTML sinks** — use `textContent`, create elements, avoid `eval`/`new Function`.
4. **Sanitise with a maintained library** if HTML input is genuinely required (DOMPurify), with an allow-list.
5. **CSP** — a strict, nonce-based `Content-Security-Policy` blocks inline script execution; strong defence in depth.
6. **Cookie flags** — `HttpOnly`, `Secure`, `SameSite=Lax/Strict`.
7. **Trusted Types** (Chromium) to make DOM sinks fail closed.

## Related

- [[Injection Attacks]]
- [[Cross-Site Request Forgery]]
- [[Session Hijacking]]
- [[OWASP Top 10]]
- [[Attacks MOC]]
