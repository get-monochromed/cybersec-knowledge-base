---
title: Privilege Escalation
aliases: [PrivEsc, Local Privilege Escalation, LPE]
category: attack
tags: [attack/host, post-exploitation, exam]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Privilege Escalation

## Summary

Going from the access you have to the access you need: user → root/SYSTEM, service account → domain admin, container → host. The pivot point between "a foothold" and "an incident".

## Linux

- **SUID/SGID binaries** — GTFOBins abuse (`find`, `vim`, `nmap --interactive`, `less` shell escape).
- **sudo misconfiguration** — `NOPASSWD`, specific binary allowed without argument restriction, `env_keep` with `LD_PRELOAD`.
- **Cron jobs** — writable scripts run by root, `PATH` hijack, wildcard injection (`tar *`).
- **Capabilities** — `cap_setuid`, `cap_dac_read_search` on a binary.
- **Writable service files / PATH** — systemd unit or script running as root that a user can edit.
- **Kernel exploits** — Dirty Pipe, Dirty COW, PwnKit (`pkexec`), OverlayFS; usually last resort after enumeration.
- **Credentials on disk** — `.bash_history`, config files, SSH keys, cloud metadata service (`169.254.169.254`).
- **Containers** — privileged container, mounted docker socket, hostPath mounts.

## Windows / Active Directory

- **Token abuse** — `SeImpersonatePrivilege` (Potato family: Juicy/Rotten/PrintSpoofer), `SeDebugPrivilege`, `SeBackupPrivilege`.
- **Misconfigured services** — unquoted service paths, weak service ACLs, writable binaries, DLL hijacking.
- **`AlwaysInstallElevated`** — MSI runs as SYSTEM.
- **Unattend files, registry creds, GPP cpassword**, `web.config` connection strings.
- **Kerberoasting / AS-REP roasting** — offline cracking of service account hashes.
- **AD ACL abuse** — `GenericAll`/`WriteDACL` on users or groups, `ForceChangePassword`, shadow credentials.
- **ADCS misconfiguration** — ESC1-style template abuse leading to domain admin.
- **DPAPI / LSASS** — credential dumping ([[Post Exploitation]]), pass-the-hash ([[Lateral Movement]]).

## Detection

- Enumeration behaviour: `whoami /priv`, `sudo -l`, `linpeas`, `winpeas`, BloodHound collection (LDAP burst queries).
- Exploit artefacts: PwnKit's `GCONV_PATH` env trick, unusual SUID execution, kernel exploit crash signatures.
- Windows: 4672 (special privileges assigned), 4688 process creation with odd parents, service creation events, token manipulation.
- EDR: process injection, LSASS access (`Sysmon` 10), named pipe creation by Potato tools.

## Mitigation

- **Patch** — kernel and setuid binaries; most LPEs are known CVEs.
- **Least privilege** — no unnecessary sudo entries, no SUID binaries, service accounts not interactive, gMSA for services.
- **Tiered administration** — separate admin accounts per tier, never browse email on a DA account ([[Authentication, Authorization and Accounting]]).
- **Application control / WDAC / AppArmor** to block unexpected binaries.
- **Credential hygiene** — LAPS, Credential Guard, no reusable local admin passwords, remove cached creds.
- **Audit AD**: BloodHound your own environment, fix ACL and ADCS misconfigurations, rotate `krbtgt` after compromise.

## Related

- [[Post Exploitation]]
- [[Lateral Movement]]
- [[Living off the Land]]
- [[Operating System Security]]
- [[Attacks MOC]]
