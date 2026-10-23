---
title: SOAR
aliases: [Security Orchestration Automation and Response, Playbooks, Automation]
category: defensive
tags: [defensive/automation]
status: developing
up: "[[Defensive Ops MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# SOAR

## Summary

Automating the repetitive 80% of incident response: enrichment, notification, containment, ticket updates. It does not replace analysts — it buys them time by removing enrichment drudgery and standardising decisions.

## Components

- **Orchestration** — call APIs across tools (EDR isolate host, firewall block IP, IdP disable account, ticketing).
- **Automation** — runbooks/playbooks triggered by an alert.
- **Case management** — incidents, tasks, evidence, collaboration.
- **Integration library** — connectors to the rest of the stack.

## Good first playbooks

1. **Phishing report** — extract URLs/headers, detonate, check sender reputation, find other recipients, quarantine, close with a template.
2. **Malware alert** — hash lookup, sandbox submit, isolate host if malicious, open a case.
3. **Suspicious login** — impossible travel check, MFA prompt analysis, force re-auth, notify user.
4. **EDR agent offline** — create a ticket, escalate after N hours.
5. **Vulnerability SLA breach** — notify asset owner and manager.

## Rules for automation

- **Automate enrichment, gate destructive actions.** Disabling accounts and isolating hosts should require approval until the playbook has a proven track record.
- **Every automated action must be logged and reversible** where possible.
- **Start with the top 3 alert types by volume**, not the most interesting ones.
- **Version control playbooks** and test them; a broken playbook is a silent failure.
- Keep a **human decision point** for anything with business impact (isolating a production server at month-end).

## Pitfalls

- Buying SOAR before fixing detection quality — you automate noise.
- API integrations with over-privileged service accounts (new risk).
- Playbooks nobody maintains as the environment changes.
- Metrics theatre: "X hours saved" without measuring whether incidents resolve better.

## Related

- [[Security Operations Centre]]
- [[SIEM]]
- [[Incident Response]]
- [[Defensive Ops MOC]]
