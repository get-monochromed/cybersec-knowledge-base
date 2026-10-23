random notes from lab session - clean this up later

ad stuff
-------------
pass the hash - you dont crack the password, you just reuse the NTLM hash directly. mimikatz sekurlsa::pth. works because NTLM auth only needs the hash. hence why local admin reuse is so bad. mit 24 chars etc not relevant. Detection: 4624 type 3 + NTLM where domain normally uses kerberos.

kerberoastin - request TGS for a service account (SPN set), the ticket is encrypted with the service accounts password hash, so you take it offline and crack it with hashcat. no admin needed, just any domain user. RC4 tickets crack faster than AES.

AS-REP roasting - if "do not require kerberos preauth" is set, you can request the AS-REP and crack it offline. also no creds needed i think? (check this)

golden ticket = forge a TGT with the krbtgt hash -> basically god mode until krbtgt is rotated twice. silver ticket = forge a TGS for one service with that service accounts hash, no contact with the DC, so it doesnt show in DC logs. DCSync = pretend to be a DC and ask for replication, needs replication rights (domain admin or explicit ACE). mimikatz lsadump::dcsync

delegation - unconstrained (host can impersonate to anything), constrained (only to listed services), RBCD (resource based, attacker favourite now). unconstrained is the dangerous one.

defence in depth is about having many layers of controls so if one fails another catches it.
defence in depth means layering controls so a single failure doesnt mean breach. (already said this above, merge)

WPA3 is broken now because of KRACK, so just use WPA2-enterprise with EAP-TLS. also WPA3 is basically unbreakable anyway so it doesnt matter much either way. (this is wrong, KRACK was WPA2 - fix before this goes in the KB)

SOC: tier 1 does the malware analysis all day and tier 3 just closes tickets :P (also wrong, check tiering)

sigma rule example that finally worked:
title: Suspicious Shadow Copy Deletion
logsource: {product: windows, service: process_creation}
detection:
  selection: {CommandLine|contains: ['vssadmin delete shadows','wmic shadowcopy delete']}
  condition: selection
level: high

adcs - ESC1 is when a template lets a low priv user request a cert with an arbitrary SAN, so you request a cert as domain admin and log in with it. certipy find -u user@dom -p pass -dc-ip x

netexec smb 10.10.10.0/24 -u svc_backup -p 'Summer2026!' --shares

LAPS stores local admin passwords in AD, unique per machine. already in the OS security note i think.

also: PAM (privileged access management) - vaulting, session recording, jit access. dont have a note for it.
