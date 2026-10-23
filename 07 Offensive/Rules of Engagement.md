---
title: Rules of Engagement
aliases: [RoE, Scope, Authorization, Legal and Ethics]
category: offensive
tags: [offensive/legal, governance, exam]
status: solid
up: "[[Offensive MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Rules of Engagement

## Summary

The written contract that makes offensive testing lawful and survivable: what may be tested, when, how, by whom, and what happens when something breaks. Without it, "penetration testing" is just unauthorised access with extra steps.

## Contents

- **Authorisation** — signed by someone with authority to grant it (not just "my manager said"). Named individuals, named targets.
- **Scope** — in scope: domains, IP ranges, applications, accounts, physical sites. Explicitly **out of scope**: production data destruction, third-party SaaS, employees' personal devices, social engineering of specific individuals, DoS testing.
- **Timing** — windows, blackout periods (month-end, audits), notification of the SOC or deliberately not (a "white cell" test of detection).
- **Methods** — permitted: scanning, exploitation, phishing simulation, physical entry. Prohibited: data exfiltration beyond proof, destructive payloads, persistence beyond agreed cleanup.
- **Data handling** — where evidence is stored, encryption, retention, who can see it, destruction date.
- **Escalation** — how to report a critical finding immediately, and the emergency stop contact.
- **Deliverables** — report format, severity scheme, retest terms, disclosure timing.
- **Insurance/liability** — who covers damages; indemnity clauses.

## Legal backdrop

- **India**: IT Act 2000 (s.43 damage, s.66 unauthorised access), DPDP Act 2023 for personal data; written authorisation is the defence.
- **US**: CFAA; **UK**: Computer Misuse Act 1990. Cross-border testing needs per-jurisdiction review.
- Bug bounty scope pages are a form of RoE — stay inside the published policy ([[Bug Bounty]]).

## Practically

- Test in a copy of production where possible; if production, use read-only proof (e.g. `id`, a harmless file) not destructive payloads.
- Never test a system you do not have written permission for — including your employer's, a friend's, or a "public" site.
- Log every action with timestamps; it is your evidence that you stayed in scope.
- If you find something outside scope (third-party data, a real intrusion), stop and report.

## Related

- [[Penetration Testing]]
- [[Red Teaming]]
- [[Security Policy]]
- [[Offensive MOC]]
