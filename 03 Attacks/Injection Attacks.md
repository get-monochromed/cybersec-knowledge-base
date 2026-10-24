---
title: Injection Attacks
aliases: [Injection, Code Injection, Command Injection]
category: attack
tags: [attack/web, owasp-a05, injection, exam]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Injection Attacks

## Summary

The largest vulnerability family: untrusted data reaches an interpreter that cannot tell data from instructions. One root cause, many interpreters — SQL, OS shell, LDAP, XPath, template engines, expression languages, deserialisers, log parsers.

## Members

| Type | Interpreter | Example sink |
|---|---|---|
| [[SQL Injection]] | database | `SELECT … WHERE id = '$id'` |
| **OS command injection** | shell | `ping -c1 $host` with `host=8.8.8.8;id` |
| **NoSQL injection** | Mongo/JSON query | `{"user": {"$ne": null}, "pass": {"$ne": null}}` |
| **LDAP injection** | directory query | `*)(uid=*))(|(uid=*` |
| **XPath injection** | XML query | `' or '1'='1` |
| **SSTI** (server-side template injection) | Jinja2/Twig/Freemarker | `{{7*7}}` → `{{config}}` → RCE |
| **EL/SpEL injection** | expression languages | `${T(java.lang.Runtime)…}` |
| **Log injection / log forging** | log files, SIEM | CRLF injection to fake entries |
| **Header/CRLF injection** | HTTP response | `%0d%0aSet-Cookie:` |
| **Deserialisation** | object deserialiser | Java `ObjectInputStream`, Python `pickle`, PHP `unserialize` |
| **Prompt injection** | LLM | data that changes model instructions (see below) |
| [[Cross-Site Scripting]] | browser JS engine | `innerHTML` |

## Why it keeps happening

Concatenating strings is the natural way to build a query, command or template. Frameworks fix the common paths, then someone writes "just this one" raw query. Also, validation is confused with sanitisation — filtering `<` does not fix a shell issue.

## Detection

- SAST patterns: `os.system`, `subprocess(..., shell=True)`, `Runtime.exec`, `eval`, `pickle.loads`, string-built queries.
- DAST: payload probes for `;`, `|`, `$()`, `{{7*7}}`, `${}`, CRLF.
- Runtime: child processes spawned by web servers (`w3wp` → `cmd.exe`, `node` → `sh`), unexpected outbound connections.

## Mitigation

- **Never build interpreter input by concatenation.** Use parameterised queries, `execve`-style APIs with argument arrays (no shell), safe template contexts, typed deserialisation allow-lists.
- **Allow-list validation** for anything that must be interpolated (IDs, enum values, filenames).
- **Least privilege**: the web process should not be able to run shells, read `/etc/shadow`, or write outside its directory. Containers help ([[Container Security]]).
- **Escape at the output layer** for the specific interpreter (HTML, SQL, shell, LDAP) — not a generic "sanitise".
- **Disable dangerous features**: no `xp_cmdshell`, no `pickle` over the network, no `${}` in user templates.

## Prompt injection (new member)

LLM inputs are an interpreter too: retrieved documents or web pages can contain instructions that hijack the model. Mitigations are immature — treat model output as untrusted, sandbox tool access, require human approval for state-changing actions, never put secrets in the system prompt.

## Related

- [[SQL Injection]]
- [[Cross-Site Scripting]]
- [[OWASP Top 10]]
- [[Application Security]]
- [[Attacks MOC]]
