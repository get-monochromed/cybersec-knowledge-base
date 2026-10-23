---
title: Digital Forensics
aliases: [Forensics, DFIR, Computer Forensics]
category: defensive
tags: [defensive/forensics, exam]
status: solid
up: "[[Defensive Ops MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Digital Forensics

## Summary

Recovering and analysing digital evidence to establish what happened, in a way that is defensible. In corporate IR the goal is scope and root cause; in legal proceedings the goal is admissibility.

## Principles

- **Preserve before you touch**: image (bit-for-bit) or capture memory before analysis; work on copies.
- **Chain of custody** — who handled what, when, where, with hashes at every transfer.
- **Order of volatility** — collect the most perishable first: CPU registers/cache → memory → network state → running processes → disk → backups/logs → archival media.
- **Document everything** — commands run, timestamps in UTC, tool versions, hashes.
- **Repeatability** — another examiner should reach the same conclusion.

## Artifacts by domain

- **Windows**: Event logs, `$MFT`, `$UsnJrnl`, registry hives (Run keys, USB history, ShimCache/AmCache), prefetch, LNK files, recycle bin, `$LogFile`, SRUM, WMI repository, memory (LSASS, injected code).
- **Linux**: `auth.log`, `journald`, bash history, cron, `~/.ssh`, systemd units, `/proc` (live), ext4 journal, auditd.
- **Network**: firewall/proxy logs, NetFlow, DNS, PCAP, TLS metadata, DHCP leases, VPN sessions.
- **Cloud**: CloudTrail/Activity Log, S3 access logs, IAM changes, container audit logs — usually the *only* evidence, and it expires.
- **Mobile**: backups, app databases, location history, chat artefacts.
- **Email**: headers, message trace, mailbox audit logs, deleted-item recovery.

## Tools

Autopsy/Sleuth Kit (disk), Volatility 3 (memory), KAPE/Velociraptor (triage and collection), Plaso/log2timeline (timeline), Eric Zimmerman tools (Windows), Wireshark (network), FTK/EnCase (commercial suites).

## Analysis techniques

- **Timeline analysis** — super-timeline of file system, event logs, and network events to reconstruct sequence.
- **Artifact correlation** — execution artefact + network connection + file creation = defensive narrative.
- **Anti-forensics awareness** — timestomping, log deletion, secure wiping, `wevtutil cl`, encrypted containers; absence of logs is itself evidence.

## Related

- [[Incident Response]]
- [[Malware Analysis]]
- [[SIEM]]
- [[Defensive Ops MOC]]
