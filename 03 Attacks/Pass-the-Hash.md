---
title: Pass-the-Hash
aliases: [PtH, Pass the Hash, Hash Reuse]
category: attack
tags: [attack/host, credential, windows, lateral]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Pass-the-Hash

## Summary

Authenticating with a captured **NTLM hash** instead of the plaintext password. The attacker never cracks anything: NTLM authentication accepts the hash directly as proof of knowledge. It is the reason local administrator password reuse turns one compromised workstation into a domain-wide incident.

## How it works

1. Obtain a hash — LSASS dump (`sekurlsa::logonpasswords`), SAM/NTDS, `reg save`, or a relayed authentication.
2. Authenticate with it — `sekurlsa::pth /user:X /ntlm:<hash> /domain:Y`, `netexec -H`, `psexec -hashes`.
3. The target sees a normal NTLM logon. No password is ever required.

The hash is the credential. NTLM challenge-response proves possession of the hash-derived key, so the plaintext is irrelevant — which is also why password *length* does not protect against PtH; only removing NTLM or preventing hash theft does.

## Related techniques

- **Pass-the-ticket (PtT)** — inject a stolen Kerberos TGT/TGS (`kerberos::ptt`) instead of an NTLM hash; often quieter in AD.
- **Overpass-the-hash** — use an NTLM hash to request a Kerberos TGT (`asktgt`), converting hash → ticket.
- **NTLM relay** — don't even steal the hash: relay the authentication to another service (`Responder` + `ntlmrelayx`).
- **Golden/silver ticket** — forged tickets are a different flavour of the same "credential is reusable material" problem ([[Golden Ticket]]).

## Detection

- **4624 logon type 3** with **NTLM** where the domain normally authenticates with Kerberos; 4624 type 9 (explicit credentials, `runas /netonly`).
- **4776** (NTLM credential validation) on the DC for accounts that should use Kerberos.
- New admin sessions from a workstation to another workstation; service creation immediately afterwards ([[Lateral Movement]]).
- EDR: LSASS access (`Sysmon` event 10), suspicious `lsass.exe` handle requests, `mimikatz`/`sekurlsa` artefacts.
- No 4768/4769 preceding access — a strong indicator that a hash or ticket was reused.

## Mitigation

- **Unique local admin passwords** — LAPS/Windows LAPS everywhere; never the same local admin hash fleet-wide.
- **Credential Guard** and LSA protection to make LSASS dumping much harder.
- **Tiered administration** — Tier 0 credentials never touch workstations ([[Authentication, Authorization and Accounting]]).
- **Disable or restrict NTLM** where the estate allows; enforce Kerberos with AES.
- **Privileged Access Management** with just-in-time admin ([[Privileged Access Management]]).
- **SMB signing + EPA** to blunt relay, and disable LLMNR/NBT-NS so `Responder` gets nothing.
- Rotate `krbtgt` and all privileged secrets after a confirmed compromise.

## Related

- NTLM (see [[Operating System Security]])
- [[Lateral Movement]]
- [[Privilege Escalation]]
- [[Kerberos]]
- [[Password Attacks]]
- [[Attacks MOC]]
