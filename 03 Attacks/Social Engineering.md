---
title: Social Engineering
aliases: [Pretexting, Human Hacking, Social Engineering Attack]
category: attack
tags: [attack/social, exam]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Social Engineering

## Summary

Manipulating people into breaking procedure or revealing information. The technical control being bypassed is always the same: a human deciding to trust. Cialdini's influence principles — authority, urgency, scarcity, social proof, reciprocity, liking — are the toolkit.

## Common forms

| Form | What it looks like |
|---|---|
| [[Phishing]] | email/SMS/voice lures (see also [[Business Email Compromise]]) |
| **Pretexting** | invented scenario ("I'm from IT, we're seeing errors on your account") |
| **Vishing** | phone call, often spoofed caller ID, sometimes with background call-centre noise |
| **Tailgating / piggybacking** | following staff through a door |
| **Shoulder surfing** | reading screens/PINs in person or on video calls |
| **Baiting** | USB drives dropped in car parks, "free" downloads |
| **Quid pro quo** | offering help to get access ("I'll fix your printer if you install this") |
| **Helpdesk / MFA reset abuse** | social-engineer the service desk into resetting MFA |
| **Watering hole** | compromise a site the target visits (see [[Supply Chain Attack]]) |
| **Scareware / tech support scam** | fake infection warnings leading to remote access |

## Advanced shapes

- **Deepfake voice/video** — CEO voice on a call authorising a transfer; increasingly cheap.
- **Multi-channel pretexting** — email, then a follow-up call that "confirms" it, then a Teams message.
- **Insider recruitment** — approaching a disgruntled employee ([[Insider Threat]]).
- **Physical pretext** — courier, inspector, fire warden, job applicant.

## Detection

Mostly human and process signals, not tooling:

- Unusual requests for credentials, MFA codes, or payment changes.
- Requests that bypass normal process "just this once", or demand secrecy.
- Slight inconsistencies: wrong internal terminology, mismatched sender display vs domain, caller unable to answer a simple challenge question.
- Helpdesk tickets: MFA reset, password reset and mailbox delegate requests are the top abuse targets.

## Mitigation

- **Process beats awareness**: verification callbacks, dual approval, challenge questions, no credential sharing policy. An employee who *can't* bypass the process cannot be tricked into it.
- **Phishing-resistant MFA** removes the value of the OTP the attacker is asking for.
- **Least privilege** limits the payoff.
- **[[Security Awareness Training]]** — realistic, short, reported-friendly; measure reporting, not just clicks.
- **Physical**: badge checks, visitor escorting, no tailgating, locked screens, clean-desk policy.
- **Culture**: people must not be punished for reporting a mistake, or they will hide it (see [[Incident Response]]).

## Related

- [[Phishing]]
- [[Business Email Compromise]]
- [[Security Awareness Training]]
- [[Insider Threat]]
- [[Attacks MOC]]
