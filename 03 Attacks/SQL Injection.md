---
title: SQL Injection
aliases: [SQLi, SQL Injection Attack]
category: attack
tags: [attack/web, owasp-a05, injection, exam]
status: solid
up: "[[Attacks MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# SQL Injection

## Summary

Untrusted input is concatenated into a SQL query, so the attacker changes the query's logic. Still the canonical injection bug: it can read, modify or delete the entire database, bypass authentication, and often escalate to OS command execution.

## How it works

```sql
-- intended
SELECT * FROM users WHERE email = 'a@b.c' AND password = 'x';

-- input: ' OR '1'='1
SELECT * FROM users WHERE email = '' OR '1'='1' AND password = '';
```

The parser cannot distinguish data from code — the same root cause as every member of [[Injection Attacks]].

## Variants

- **In-band / classic** — results visible in the response:
  - **Union-based** — `' UNION SELECT username, password FROM users-- -` (needs matching column count/types).
  - **Error-based** — force a database error that leaks data (`extractvalue`, `CAST`).
- **Blind** — no output, only true/false or timing:
  - **Boolean-based** — `' AND 1=1-- -` vs `' AND 1=2-- -`.
  - **Time-based** — `'; IF (1=1) WAITFOR DELAY '0:0:5'-- -` (MSSQL), `SLEEP(5)` (MySQL), `pg_sleep(5)`.
- **Out-of-band** — exfiltrate via DNS/HTTP (works when nothing is echoed).
- **Second-order** — payload stored safely, executed later by another query (e.g. in an admin report).
- **Stacked queries** — `; DROP TABLE users-- -` where the driver allows multiple statements.

Auth bypass, data exfiltration, file read/write (`LOAD_FILE`, `INTO OUTFILE`), command execution (`xp_cmdshell`), and in some stacks full host compromise.

## Detection

- **Code review/SAST**: string concatenation into queries, f-strings/`+`/`format()` in SQL, string-built `ORDER BY`.
- **DAST/[[WAF]]**: payload probes (`'`, `"`, `--`, `UNION`, `SLEEP`) and error signatures.
- **Logs**: SQL error messages in responses, anomalous query patterns, unusually long parameters, `information_schema` and `sqlmap` user-agent strings.
- Prevention is verifiable: parameterised queries make the bug structurally impossible.

## Mitigation

1. **Parameterised queries / prepared statements** — the real fix. Input becomes data, never syntax.
2. **ORMs correctly used** — raw query escape hatches reintroduce the bug.
3. **Allow-list validation** — for identifiers that cannot be parameterised (`ORDER BY` column, table name).
4. **Least-privilege DB accounts** — no `FILE`, no `xp_cmdshell`, no DDL for the web app user. Limits blast radius after a miss.
5. **Error handling** — generic errors to users, detail to logs.
6. **WAF** — defence in depth, not a fix (encoding bypasses exist).
7. **Secrets hygiene** — hashed passwords ([[Hashing]]) so a dump is not instantly game over.

## Related

- [[Injection Attacks]]
- [[OWASP Top 10]]
- [[Web Application Security]]
- [[Broken Access Control]]
- [[Attacks MOC]]
