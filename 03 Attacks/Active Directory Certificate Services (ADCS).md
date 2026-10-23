---
title: Active Directory Certificate Services (ADCS)
aliases: [ADCS, ESC1, ESC8, AD CS Abuse, Certipy]
category: attack
tags: [attack/host, active-directory, pki, privilege]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Active Directory Certificate Services (ADCS)

## Summary

ADCS is Microsoft's PKI: it issues certificates that Windows treats as authentication credentials (PKINIT, smart-card logon, mTLS). Because a certificate can authenticate as the identity in its Subject Alternative Name, a misconfigured template is a direct path to domain admin — and certificates survive password resets.

## Why certificates are special

- Authentication is based on the certificate, not a password — so **rotating a password does not revoke attacker access**.
- Validity is typically **1–10 years**.
- The CA's private key signs everything; compromise of the CA is compromise of the domain.
- Template and CA permissions are rarely reviewed, because "PKI is infrastructure".

## The ESC families (selected)

| ID | Flaw | Result |
|---|---|---|
| **ESC1** | Template allows **enrollee-supplied subject** + client-auth EKU + low-priv enrollee | Request a cert with `SAN: administrator`, authenticate as that user |
| **ESC2** | Template allows any purpose / no EKU | Same, via any-purpose certificate |
| **ESC3** | Enrolment agent template abuse | Request a cert on behalf of anyone |
| **ESC4** | Writable template ACLs | Rewrite a template into ESC1 |
| **ESC6** | `EDITF_ATTRIBUTESUBJECTALTNAME2` on the CA | SAN for any template |
| **ESC7** | CA officer/manage rights | Approve or issue your own requests |
| **ESC8** | HTTP enrolment + NTLM relay | Relay a coerced machine/user auth to the CA's `/certsrv` and get a DC certificate |
| **ESC9–ESC15** | Various (no security extension, certificate mapping, SID in SAN) | Incremental bypasses of patches |

Discovery: `certipy find -u user@corp.local -p pass -dc-ip DC -vulnerable`.

## Attack flow (ESC1)

1. Find a template with `ENROLLEE_SUPPLIES_SUBJECT`, client authentication EKU, and enrollee rights for `Domain Users`.
2. Request with an arbitrary SAN: `certipy req -ca CORP-CA -template Vuln -upn administrator@corp.local`.
3. Authenticate with PKINIT: `certipy auth -pfx administrator.pfx -dc-ip DC` → get a TGT (and often the NT hash via UnPAC-the-hash).
4. Domain admin, no password needed.

## Detection

- Certificate issuance events (**4886/4887** on the CA) for templates that should never be requested, and for SANs that do not match the requester.
- Requests where the SAN contains a privileged account or a different user than the requester.
- **ESC8**: NTLM authentication to the CA's HTTP enrolment endpoint from a non-member host; relay tooling artefacts.
- New or modified templates (`msPKI-*` attribute changes), CA-wide settings changes.
- Unusual PKINIT logons (4768 with certificate pre-auth) for accounts that normally use passwords.

## Mitigation

- Remove **enrollee-supplied subject** from templates; require manager approval for privileged templates.
- Restrict enrolment permissions to the groups that need the template; audit template ACLs.
- Enable **CA certificate policies** ("strong certificate mapping"), apply the relevant Windows updates, and set `szOID_NTDS_CA_SECURITY_EXT` enforcement.
- **Disable HTTP enrolment**; require HTTPS with EPA (extended protection for authentication) and no NTLM on the CA.
- Isolate the CA as **Tier 0**; its admin is a domain admin equivalent.
- Monitor the CA continuously and treat any certificate issued for `administrator` as an incident.

## Related

- [[Kerberos Delegation]]
- [[Privilege Escalation]]
- [[Digital Signatures and PKI]]
- [[Operating System Security]]
- [[Attacks MOC]]
