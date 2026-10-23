---
title: Security Tools
aliases: [Tooling, Pentest Tools, Tool Index]
category: offensive
tags: [offensive/tools, reference]
status: developing
up: "[[Offensive MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Security Tools

## Summary

Index of tools by task, plus what each is actually for. Tools are not methodology — but knowing the right one saves hours.

## Recon and OSINT

- `nmap`, `masscan` — port/host discovery.
- `subfinder`, `amass`, `assetfinder` — subdomain enumeration.
- `crt.sh`, `dnsx`, `dig` — DNS and certificate transparency.
- `theHarvester`, `Maltego`, `SpiderFoot` — OSINT aggregation.
- Shodan / Censys / FOFA — internet exposure search.
- `gobuster`, `ffuf`, `feroxbuster` — content and vhost discovery.
- `waybackurls`, `gau` — historical URLs.

## Web

- **Burp Suite** (Community/Pro) — interception, repeater, intruder, scanner.
- `OWASP ZAP` — free alternative, automation-friendly.
- `sqlmap` — SQLi detection/exploitation.
- `nuclei` — template-based CVE/misconfig scanning.
- `nikto` — quick web server checks.
- `jwt_tool`, `Postman`/`Insomnia` — API testing.
- `XSStrike`, `dalfox` — XSS automation.

## Exploitation and post-exploitation

- `Metasploit` — framework, modules, sessions, pivoting.
- `Impacket` — Windows protocol tooling (`secretsdump`, `wmiexec`, `psexec`).
- `NetExec`/`CrackMapExec` — SMB/WinRM/LDAP swiss army knife.
- `BloodHound` + `SharpHound` — AD attack-path mapping.
- `Mimikatz` — credential extraction (and detection research).
- `Responder` — LLMNR/NBT-NS/mDNS poisoning.
- `hashcat`, `john` — offline cracking.
- `hydra`, `medusa` — online credential attacks.
- `Sliver`, `Mythic`, `Havoc`, `Cobalt Strike` — C2 frameworks.
- `chisel`, `ligolo-ng`, `socat` — tunnelling and pivoting.

## Network

- **Wireshark**/`tshark` — packet analysis.
- `tcpdump` — capture on hosts.
- `Responder`, `Bettercap` — MITM on LAN.
- `aircrack-ng`, `hcxdumptool`, `bettercap` — Wi-Fi.
- `Suricata`, `Zeek`, `Snort` — network detection (defensive).

## Defensive / blue

- `Wazuh`, `ELK`/`OpenSearch`, `Splunk`, `Sentinel` — SIEM.
- `Sigma` — vendor-neutral detection rules.
- `YARA` — file/memory signatures.
- `Velociraptor`, `GRR`, `KAPE` — endpoint triage/forensics.
- `Autopsy`, `Volatility`, `Sleuth Kit` — forensics.
- `Atomic Red Team`, `Caldera` — purple teaming.

## Analysis

- `Ghidra`, `IDA`, `x64dbg`, `dnSpy`, `JADX` — reverse engineering.
- `CyberChef` — encoding/decoding swiss army knife.
- VirusTotal, Any.Run, Hybrid Analysis — sample triage.

## Lab

Kali/Parrot for offence, REMnux/FlareVM for analysis, a segmented virtual network. Never test against systems you do not own ([[Rules of Engagement]]).

## Related

- [[Scanning and Enumeration]]
- [[Exploitation]]
- [[Malware Analysis]]
- [[Command Cheatsheet]]
- [[Offensive MOC]]
