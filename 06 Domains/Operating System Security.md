---
title: Operating System Security
aliases: [Windows Security, Linux Security, OS Hardening, Active Directory Security]
category: domain
tags: [domain/host, hardening]
status: solid
up: "[[Domains MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Operating System Security

## Summary

The host layer: accounts, permissions, services, patching, logging. Most real intrusions end up here, and most privilege escalation lives here too ([[Privilege Escalation]]).

## Windows

- **Active Directory is the crown jewel.** Domain admin = everything. Tiered admin, LAPS, Protected Users, Credential Guard, `krbtgt` rotation after compromise.
- Harden: disable SMBv1/LLMNR/NBT-NS, enforce LDAP signing/channel binding, restrict NTLM, LAPS for local admin, Windows LAPS/Defender Firewall default-deny.
- Attack surface: RDP exposed, unconstrained delegation, ADCS misconfigurations, GPP cpassword, printers (PrintNightmare), vulnerable drivers (BYOVD).
- Logging: 4624/4625 (logon), 4688 (process), 4672 (privilege), 7045 (service install), Sysmon, PowerShell 4104. Forward to [[SIEM]] — local logs are attacker-editable.

## Linux

- Accounts: no direct root login, `sudo` least privilege with specific commands, no shared accounts, SSH keys with passphrases and `authorized_keys` hygiene.
- Harden: disable unused services, mount `/tmp` with `noexec,nosuid`, SELinux/AppArmor enforcing, auditd, unattended security updates.
- Attack surface: SUID binaries, cron jobs, writable service files, exposed Docker socket, kernel version.
- Logging: `auditd`, `journald` forwarding, `sudo` logs, auth.log, file integrity monitoring (AIDE).

## Cross-platform

- Full-disk encryption with TPM, Secure Boot, screen lock, USB control.
- EDR agent healthy and tamper-protected ([[Endpoint Protection]]).
- Patch cadence with reboot verification ([[Patch Management]]).
- Baseline against CIS Benchmarks; detect drift.

## Related

- [[Hardening]]
- [[Privilege Escalation]]
- [[Lateral Movement]]
- [[Endpoint Protection]]
- [[Domains MOC]]
