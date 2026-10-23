---
title: Glossary
aliases: [Terms, Definitions]
category: reference
tags: [reference, glossary]
status: solid
up: "[[Reference MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Glossary

One line per term, with the note to read for depth.

## Foundations

**Asset** — anything of value worth protecting: data, service, reputation, people. → [[Risk Management]]
**Attack surface** — every interface an attacker can reach. → [[Attack Surface]]
**Attack vector** — the path used to reach and exploit a target (email, exposed service, USB).
**Control** — a safeguard that changes likelihood or impact. → [[Security Controls]]
**Defence in depth** — independent layers so one failure is not fatal. → [[Defence in Depth]]
**Least privilege** — minimum access, minimum time. → [[Security Principles]]
**Residual risk** — risk remaining after controls. → [[Risk Management]]
**Threat** — a potential cause of harm. → [[Vulnerability, Threat, Risk and Exploit]]
**Threat actor** — who might act against you. → [[Threat Actor]]
**Trust boundary** — a line where trust level changes. → [[Trust Boundaries]]
**Vulnerability** — a weakness that can be exploited. → [[Vulnerability, Threat, Risk and Exploit]]
**Zero day** — a vulnerability with no vendor fix (and often no public knowledge) at time of use. → [[Exploitation]]

## Attacks and malware

**Backdoor / implant** — persistent remote access mechanism. → [[Trojan]]
**Botnet** — network of compromised hosts under remote control. → [[Botnet]]
**Brute force** — trying many credentials. → [[Password Attacks]]
**Credential stuffing** — replaying breached username/password pairs. → [[Password Attacks]]
**Drive-by download** — malware installed just by visiting a page.
**Dropper** — minimal malware whose job is to install the real payload. → [[Malware]]
**Evil twin** — lookalike Wi-Fi AP. → [[Wireless Attacks]]
**Exploit** — code/technique that leverages a vulnerability. → [[Exploitation]]
**Fileless malware** — payload living in memory/registry/scripts. → [[Fileless Malware]]
**IDOR** — insecure direct object reference; accessing another user's object by changing an ID. → [[Broken Access Control]]
**Implant** — see backdoor.
**Infostealer** — malware harvesting credentials, cookies, wallets. → [[Spyware and Keyloggers]]
**Initial access broker** — sells compromised footholds. → [[Cybercriminal]]
**Lateral movement** — moving host-to-host after compromise. → [[Lateral Movement]]
**Living off the land** — abusing legitimate OS tools. → [[Living off the Land]]
**Logic bomb** — dormant code triggered by a condition. → [[Malware]]
**Malware** — software with malicious or unauthorised behaviour. → [[Malware]]
**MITM** — attacker positioned between two parties. → [[Man-in-the-Middle (MITM)]]
**Persistence** — mechanism that survives reboot/logout. → [[Post Exploitation]]
**Phishing** — deception to induce a click/credential/action. → [[Phishing]]
**Pivot** — using a compromised host to reach another network. → [[Lateral Movement]]
**Privilege escalation** — gaining higher rights. → [[Privilege Escalation]]
**Ransomware** — malware denying access for extortion. → [[Ransomware]]
**RAT** — remote access trojan. → [[Trojan]]
**Rootkit** — malware that hides itself. → [[Rootkit]]
**Spear phishing** — targeted phishing. → [[Phishing]]
**Spraying** — one password tried across many accounts. → [[Password Attacks]]
**Supply chain attack** — compromising a trusted dependency or vendor. → [[Supply Chain Attack]]
**Trojan** — malware disguised as legitimate software. → [[Trojan]]
**Wiper** — malware destroying data. → [[Malware]]
**Worm** — self-propagating network malware. → [[Worm]]
**XSS** — injected JavaScript executing in a victim's browser. → [[Cross-Site Scripting]]
**Zip bomb** — archive that expands enormously, exhausting resources. → [[Denial of Service (DoS)]]

## Active Directory and Kerberos

**ADCS** — Active Directory Certificate Services; issues certs that authenticate as a user. → [[Active Directory Certificate Services (ADCS)]]
**AS-REP roasting** — cracking the AS-REP of an account without pre-auth. → [[AS-REP Roasting]]
**DCSync** — abusing replication rights to pull password hashes from a DC. → [[DCSync]]
**ESC1** — vulnerable ADCS template allowing an attacker-chosen SAN. → [[Active Directory Certificate Services (ADCS)]]
**Golden ticket** — forged TGT signed with the krbtgt hash. → [[Golden Ticket]]
**gMSA** — group managed service account; machine-managed 240-char password.
**Kerberoasting** — cracking a service ticket offline. → [[Kerberoasting]]
**krbtgt** — the account whose hash signs every TGT; compromise = domain compromise. → [[Kerberos]]
**LAPS** — Local Administrator Password Solution; unique local admin passwords per host. → [[Operating System Security]]
**Pass-the-hash** — authenticating with an NTLM hash instead of a password. → [[Pass-the-Hash]]
**Pass-the-ticket** — injecting a stolen Kerberos ticket. → [[Pass-the-Hash]]
**RBCD** — resource-based constrained delegation. → [[Kerberos Delegation]]
**Silver ticket** — forged service ticket signed with a service account key. → [[Silver Ticket]]
**SPN** — Service Principal Name; how Kerberos names a service. → [[Kerberos]]
**TGT** — ticket granting ticket, obtained from the AS. → [[Kerberos]]
**TGS** — service ticket, obtained from the TGS for a specific SPN. → [[Kerberos]]

## Defence and operations

**Alert fatigue** — desensitisation from too many low-quality alerts. → [[Security Operations Centre]]
**Chain of custody** — documented evidence handling trail. → [[Digital Forensics]]
**Containment** — stopping spread during an incident. → [[Incident Response]]
**CSPM** — cloud security posture management. → [[Cloud Security]]
**Detection engineering** — building and maintaining detections as code. → [[Purple Teaming]]
**Dwell time** — time an attacker is present before detection. → [[Security Operations Centre]]
**EDR** — endpoint detection and response. → [[Endpoint Protection]]
**Eradication** — removing attacker presence. → [[Incident Response]]
**Honeytoken** — fake credential/file whose use signals compromise. → [[Honeypot]]
**IOC** — indicator of compromise. → [[Indicators of Compromise]]
**MDR** — managed detection and response. → [[Security Operations Centre]]
**Microsegmentation** — per-workload network policy. → [[Network Segmentation]]
**MTTD/MTTA/MTTR** — mean time to detect/acknowledge/respond. → [[Security Operations Centre]]
**Sigma rule** — vendor-neutral YAML detection rule. → [[Sigma Rules]]
**Playbook** — predefined response procedure. → [[SOAR]]
**Post-incident review** — structured lessons-learned after an incident. → [[Incident Response]]
**Purple teaming** — red and blue collaborating on detection coverage. → [[Purple Teaming]]
**SOAR** — orchestration and automation platform. → [[SOAR]]
**Threat hunting** — proactive search for undetected compromise. → [[Threat Hunting]]
**TTP** — tactics, techniques and procedures. → [[MITRE ATT&CK]]
**UEBA** — user/entity behaviour analytics. → [[SIEM]]
**ZTNA** — zero trust network access. → [[Zero Trust Architecture]]

## Cryptography

**AEAD** — authenticated encryption with associated data. → [[Symmetric Encryption]]
**Ciphertext** — encrypted output.
**Digital signature** — cryptographic proof of origin and integrity. → [[Digital Signatures and PKI]]
**Forward secrecy** — past sessions safe if long-term key leaks. → [[TLS]]
**Hash** — fixed-size one-way digest. → [[Hashing]]
**HMAC** — keyed hash for integrity/authenticity. → [[Hashing]]
**KDF** — key derivation function (incl. password hashing). → [[Hashing]]
**Nonce / IV** — value used once per key. → [[Symmetric Encryption]]
**PFS** — perfect forward secrecy. → [[TLS]]
**PKI** — public key infrastructure. → [[Digital Signatures and PKI]]
**Plaintext** — unencrypted data.
**Salt** — unique random value added before hashing a password. → [[Hashing]]
**Steganography** — hiding data inside other data (images, audio).
**X.509** — certificate format used by TLS. → [[Digital Signatures and PKI]]

## GRC

**BCP/DR** — business continuity / disaster recovery. → [[Business Continuity and Disaster Recovery]]
**Data fiduciary** — DPDP term for the entity deciding processing. → [[DPDP Act 2023]]
**DPIA** — data protection impact assessment. → [[GDPR]]
**ISMS** — information security management system. → [[ISO 27001]]
**RTO/RPO** — recovery time/point objective. → [[Backup and Recovery]]
**SoA** — Statement of Applicability (ISO 27001). → [[ISO 27001]]
**SDF** — Significant Data Fiduciary (DPDP). → [[DPDP Act 2023]]

## Related

- [[Acronyms]]
- [[Reference MOC]]
