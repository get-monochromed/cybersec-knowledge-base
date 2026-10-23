---
title: Security Awareness Training
aliases: [Awareness Training, Security Training, Phishing Simulation]
category: defence
tags: [defence/people, social]
status: solid
up: "[[Defences MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Security Awareness Training

## Summary

Changing human behaviour so people do not become the vulnerability. The goal is not "know what phishing is" — everyone knows — but reliable *reporting* and *procedure adherence* under pressure.

## What works

- **Short, frequent, contextual** training (microlearning) instead of a 90-minute annual video.
- **Realistic simulations** with immediate, non-punitive feedback. Track **report rate** as the primary metric; click rate matters but reporting is what accelerates response.
- **One-click report button** in the mail client, with feedback to the reporter ("you were the first to report this, it was malicious"). This is the highest-value single change.
- **Role-based content**: finance gets BEC/[[Business Email Compromise]]; IT gets credential handling; executives get whaling and travel risks; developers get secure coding ([[Application Security]]).
- **Process reinforcement**: training alone cannot fix a process that forces users to bypass controls ([[Social Engineering]]).

## What does not work

- Blame and punishment for clicks — drives concealment, delays response.
- Generic compliance-only modules with a quiz at the end.
- Awareness as the *only* phishing control: technical controls ([[Email Security]], phishing-resistant MFA) do the heavy lifting.
- Measuring completion rates as if they were effectiveness.

## Programme shape

1. Baseline: current report rate, click rate, ticket volume.
2. Baseline technical controls so users are not the only line of defence.
3. Run quarterly simulations with varied pretexts (invoice, HR, voicemail, QR).
4. Close the loop publicly: "this campaign, X% reported."
5. Train the specific gaps found in real incidents, not a fixed curriculum.

## Metrics

- Time to first report (target: minutes).
- Report rate vs click rate over time.
- Repeat clickers — coach individually, do not punish.
- Helpdesk social-engineering resistance (test MFA reset verification).

## Related

- [[Phishing]]
- [[Social Engineering]]
- [[Insider Threat]]
- [[Incident Response]]
- [[Defences MOC]]
