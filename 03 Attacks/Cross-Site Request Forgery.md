---
title: Cross-Site Request Forgery
aliases: [CSRF, XSRF, Session Riding]
category: attack
tags: [attack/web, owasp, exam]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Cross-Site Request Forgery

## Summary

Forcing a logged-in user's browser to send a state-changing request to another site where they are authenticated. The browser automatically attaches cookies, so the target cannot tell the request was not intentional — unless the request carries something a cross-site page cannot forge.

## How it works

1. Victim is authenticated to `bank.com` (session cookie).
2. Victim visits `evil.com`, which contains `<img src="https://bank.com/transfer?to=attacker&amount=5000">` (or an auto-submitting form for POST).
3. The browser sends the request with `bank.com` cookies attached.
4. The server sees a valid session and executes the transfer.

GET requests with side effects are trivially exploitable this way. POST-only endpoints are still forgeable via auto-submitting forms.

## Variants

- **Login CSRF** — force the victim into the attacker's account, then observe their activity.
- **JSON CSRF** — some stacks accept `text/plain` bodies that a form can send.
- **XSS-assisted** — XSS can read the CSRF token, so XSS defeats CSRF defences ([[Cross-Site Scripting]]).
- **GraphQL / API CSRF** — endpoints that authenticate by cookie and accept simple content types.

## Detection

- Requests lacking `Origin`/`Referer` where the app expects same-site.
- CSRF token absent, reused across sessions, or not bound to user.
- Cross-origin `POST`/`PUT`/`DELETE` in proxy logs with cookie auth and no token.

## Mitigation

1. **`SameSite=Lax` (or `Strict`) cookies** — default in modern browsers, blocks most cross-site sends. `None` requires `Secure` and reopens the risk.
2. **Synchroniser token** — unpredictable per-session (or per-request) token checked server-side, ideally double-submit with a signed cookie.
3. **Custom header requirement** (`X-Requested-With`) or JSON content-type enforcement — cross-origin pages cannot set these without CORS approval.
4. **Origin/Referer validation** on state-changing requests.
5. **No state change on GET** — idempotent GET, side effects on POST/PUT/DELETE.
6. **Re-authentication for sensitive actions** (password change, payment, email change).

Note: token-based APIs in an `Authorization` header are not automatically CSRF-equivalent, but storing tokens in cookies reintroduces the problem.

## Related

- [[Cross-Site Scripting]]
- [[Session Hijacking]]
- [[Injection Attacks]]
- [[OWASP Top 10]]
- [[Attacks MOC]]
