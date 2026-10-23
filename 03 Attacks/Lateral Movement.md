---
title: Lateral Movement
aliases: [East-West Movement, Pivoting]
category: attack
tags: [attack/host, post-exploitation]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Lateral Movement

## Summary

Moving from the initially compromised host to other systems, using stolen credentials and legitimate admin tools. This is where a single phished laptop becomes a domain-wide [[Ransomware]] event — and why flat networks are the biggest single risk multiplier.

## Techniques

- **Pass-the-hash / pass-the-ticket** — reuse NTLM hashes or Kerberos tickets without cracking passwords ([[Post Exploitation]]).
- **RDP** — interactive login with valid credentials; often to a jump host.
- **SMB / PsExec / `smbexec`** — service creation on a remote host; `net use` to admin shares.
- **WMI / WinRM** — `wmic /node:`, `Invoke-Command`; blends with admin activity.
- **Scheduled tasks** — remote task creation for execution.
- **SSH with stolen keys** — common in Linux estates and cloud.
- **Cloud control plane** — IAM role assumption, `sts:AssumeRole` chains, azure managed identity abuse.
- **Pivoting** — using a compromised host as a proxy (`ssh -D`, Chisel, SOCKS) to reach otherwise unreachable segments.
- **Credential dumping** at each hop — LSASS, SAM, LSA secrets, browser creds, config files.

## Detection

- **Authentication anomalies**: 4624 logon type 3/10 between workstations, NTLM logons where Kerberos is the norm, admin account logging into a workstation it never touches.
- **Remote execution artefacts**: service creation (7045) right after a logon, `PSEXESVC` service, `WmiPrvSE.exe` spawning a shell.
- **Lateral tooling**: Cobalt Strike default named pipes, Impacket's `smbexec`/`wmiexec` patterns, `net.exe use` bursts.
- **Honeytokens** — a fake admin account or service; any use is high-fidelity.
- Graph analysis over authentication logs: fan-out from a single host ([[SIEM]]).

## Mitigation

- **Segmentation** — workstations cannot talk to workstations; servers only from admin VLANs/PAWs ([[Network Segmentation]]).
- **Tiered admin model** — Tier 0 (AD/CA), Tier 1 (servers), Tier 2 (workstations); credentials never cross downward.
- **LAPS** for local admin passwords, unique per host; disable local admin reuse.
- **Credential Guard / LSA protection** on Windows, `Protected Users` group, disable NTLM where feasible.
- **Block legacy protocols** — SMBv1, LLMNR/NBT-NS (responder bait), WDigest.
- **Restrict RDP** with jump hosts, MFA, and session recording; no workstation-to-workstation RDP.
- **Just-in-time / just-enough admin** (PAM) instead of permanent domain admin ([[Zero Trust Architecture]]).
- Detection is the fallback: assume a foothold exists and make every hop loud.

## Related

- [[Post Exploitation]]
- [[Privilege Escalation]]
- [[Network Segmentation]]
- [[Zero Trust Architecture]]
- [[Ransomware]]
- [[Attacks MOC]]
