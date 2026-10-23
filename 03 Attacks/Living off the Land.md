---
title: Living off the Land
aliases: [LOTL, LOLBins, Living off the Land Binaries]
category: attack
tags: [attack/host, evasion, detection]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Living off the Land

## Summary

Using tools already present on the target OS instead of dropping custom malware: PowerShell, `certutil`, `rundll32`, `wmic`, `bitsadmin`, `mshta`, `bash`, `cron`, `curl`. Nothing new appears on disk, so signature-based AV and "is this file known-bad?" checks see nothing.

## Why it works

- Binaries are **signed and expected**, so allow-lists often permit them.
- Activity looks like administration, so it blends into noise.
- Requires no malware development and survives cleanup that removes dropped files.

## Common binaries (Windows)

| Binary | Abused for |
|---|---|
| `powershell.exe` | download cradles (`IEX (New-Object Net.WebClient).DownloadString(...)`), encoded commands, AMSI bypass |
| `certutil.exe` | download (`-urlcache -f`), base64 decode |
| `bitsadmin` / `Start-BitsTransfer` | stealthy download, persistence |
| `mshta.exe` | execute remote HTA, bypass app control |
| `rundll32.exe` / `regsvr32.exe` | proxy execution, `scrobj.dll` scriptlets (Squiblydoo) |
| `wmic.exe` | remote execution, process creation, AV enumeration |
| `schtasks.exe` | persistence |
| `msbuild.exe`, `installutil.exe` | execute C# without a normal compiler |
| `ntdsutil`, `vssadmin`, `esentutl` | credential/AD database copy, shadow copy deletion |

Linux equivalents: `bash -c`, `curl`/`wget`, `python3`, `socat`, `nc`, `systemctl`, `crontab`, `openssl` (encrypted C2), `awk`/`perl` for scripting.

## Detection

Detection must be **behavioural**, not file-based:

- **Command-line logging** — Windows 4688 with command line, PowerShell 4104 script block logging, Sysmon 1.
- **Parent-child anomalies** — `winword.exe` → `powershell.exe`, `w3wp.exe` → `cmd.exe`, `services.exe` → `rundll32.exe`.
- **Encoded/obfuscated commands** — `-enc`, `-nop`, `-w hidden`, `FromBase64String`.
- **Network from unexpected processes** — `certutil`, `bitsadmin`, `regsvr32` making HTTP requests.
- **Rarity analysis** — process command lines not seen in the rest of the fleet ([[SIEM]], EDR).

## Mitigation

- **Application control** (WDAC/AppLocker) restricting script hosts and binary paths; PowerShell in Constrained Language Mode.
- **AMSI** enabled everywhere (and patched — bypasses are common); script block logging on.
- **Disable unused features**: `wmic` (deprecated), `mshta`, Office macros from the internet, PowerShell v2.
- **Egress control** so a download cradle has nowhere to fetch from.
- **EDR with behavioural rules** rather than AV signatures; [[Threat Hunting]] for these patterns.
- Accept residual risk: LOTL cannot be fully blocked, only made noisy.

## Related

- [[Post Exploitation]]
- [[Lateral Movement]]
- [[MITRE ATT&CK]]
- [[Endpoint Protection]]
- [[Attacks MOC]]
