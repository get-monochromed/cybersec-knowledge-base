---
title: Command Cheatsheet
aliases: [Cheatsheet, Commands, CLI Reference]
category: reference
tags: [reference, tools]
status: developing
up: "[[Reference MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Command Cheatsheet

Only commands worth remembering. Man pages for the rest.

## Network

```bash
ip a; ip r                       # interfaces, routes
ss -tulpn                        # listening sockets + process
dig +short example.com MX        # DNS query
dig AXFR @ns.example.com dom.tld # zone transfer (recon)
tcpdump -ni eth0 -w cap.pcap 'port 443'
curl -sv https://host            # headers + TLS handshake
openssl s_client -connect host:443 -servername host -tls1_3
nmap -sV -sC -p- host            # full scan
```

## Linux triage

```bash
last -a; who; w                  # logins
ps auxf; pstree -p               # processes
lsof -i -P -n                    # network per process
find / -perm -4000 -type f 2>/dev/null   # SUID binaries
sudo -l                          # sudo rights
crontab -l; ls -la /etc/cron*    # persistence
systemctl list-units --failed
journalctl -u ssh --since "1 hour ago"
getent passwd | awk -F: '$3>=1000'       # human users
```

## Windows triage (PowerShell)

```powershell
Get-Process | Sort CPU -Desc | Select -First 20
Get-NetTCPConnection -State Listen
Get-LocalUser; Get-LocalGroupMember Administrators
Get-WinEvent -FilterHashtable @{LogName='Security';Id=4624,4625} -MaxEvents 50
Get-ScheduledTask | Where State -ne Disabled
Get-CimInstance Win32_Service | Where StartMode -eq 'Auto'
net user; net localgroup administrators
```

## Crypto

```bash
sha256sum file; openssl dgst -sha256 file
openssl rand -hex 32                    # key material
openssl enc -aes-256-gcm -in f -out f.enc   # prefer age/sops in practice
base64 -d <<< "c3RyaW5n"
```

## Detection / analysis

```bash
strings -a sample | less
file sample; sha256sum sample
yara -r rules.yar /path
grep -rEi 'password|secret|api[_-]?key' . --include='*.env'
```

## Git safety

```bash
git log --all --oneline -- '*secret*'
gitleaks detect --source . --report-format json
git filter-repo --path secrets.txt --invert-paths   # after rotation
```

## Related

- [[Security Tools]]
- [[Scanning and Enumeration]]
- [[Digital Forensics]]
- [[Reference MOC]]
