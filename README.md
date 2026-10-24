---
title: README
aliases: [Vault Guide, Conventions]
category: meta
tags: [meta, workflow]
status: solid
created: 2026-10-23
updated: 2026-10-23
---

# How this vault works

> [!warning] This vault is public
> It is published at `github.com/get-monochromed/cybersec-knowledge-base` and every commit is world-readable. It contains only generic, textbook cyber-security knowledge. Before ingesting anything, read the "Public repository rules" section below.

A personal cyber-security Wikipedia. Folders give the coarse map, wikilinks give the real graph, frontmatter makes everything queryable with Dataview.

## Layout

```
CyberSec/
├── Home.md              dashboard
├── Unorganised/         inbox — raw braindumps, clippings, half-thoughts
├── _Archive/            sources after they have been ingested (never deleted)
├── _Templates/          note skeletons (Templater)
├── _Attachments/        images, PDFs, diagrams
├── 01 Foundations/      …
└── 11 Reference/
```

`Unorganised/` is a **queue, not storage**. After a braindump has been refactored into the right section, the source file moves to `_Archive/` with an `ingested: true` marker so nothing is lost and nothing is duplicated.

## Note conventions

- **One concept per note.** If a note needs two H1s, it is two notes.
- **Filename = title**, Title Case, unique across the whole vault. Disambiguate with parentheses: `Denial of Service (DoS).md`.
- **Section hub**: every folder has a `<Section> MOC` note listing its children. New notes get linked into it — no orphans.
- **Every note ends with `## Related`** containing 3–8 sibling wikilinks. A note with no inbound and no outbound links is a bug.
- **Aliases** go in frontmatter so `[[SQLi]]` resolves to `SQL Injection`.
- Explain acronyms on first use; the glossary is for reference, not for hiding meaning.

## Frontmatter schema

```yaml
---
title: SQL Injection
aliases: [SQLi]
category: attack          # foundation | actor | attack | malware | defence | domain | offensive | defensive | grc | crypto | reference
tags: [attack/web, owasp-a05, injection]
status: solid             # stub | developing | solid
created: 2026-10-23
updated: 2026-10-23
sources: []               # URLs, books, course names
---
```

`status` drives the maintenance queries: `stub` = a link and a sentence, `developing` = useful but incomplete, `solid` = you could answer an interview question from it.

## Tagging

Tags are cross-cutting, folders are primary. Prefixes:

- `attack/web`, `attack/network`, `attack/social`, `attack/host`
- `defence/network`, `defence/endpoint`, `defence/detection`
- `actor/…`, `malware/…`, `crypto/…`, `grc/…`, `domain/…`
- `owasp-a01`…`owasp-a10`, `mitre-ta0001`… for framework mapping
- `exam` for things worth memorising

## Ingest workflow

1. Dump into `Unorganised/` — no formatting rules, plain text is fine.
2. Ask Pi to ingest it (`/kb:ingest`, or "ingest Unorganised").
3. Pi produces a **filing plan**: which notes it creates, which it merges into, which links it adds.
4. Approve, then it writes, updates the MOCs, and moves sources to `_Archive/`.
5. Weekly: run the health queries on [[Home]] and fix anything `stub`.

## Plugins in use

Templater, QuickAdd, Dataview, Breadcrumbs, Janitor, Linter, Obsidian Git, Excalidraw, Smart Connections, Spaced Repetition, Omnisearch, Local REST API, Table Editor.

Templater template folder: `_Templates`. Breadcrumbs reads the `up:` frontmatter field (every note points at its section MOC) alongside the wikilinks.

**Obsidian Git is installed but disabled.** Automatic commits are off, so nothing gets published without a human decision. Use the helper instead:

```bash
cybersec-push                 # shows changes, asks for a commit message, pushes
cybersec-push "message here"  # non-interactive, for agents and scripts
```

It lives at `~/.local/bin/cybersec-push`, refuses to commit content that looks like a private key or API token, and reports pushed commits. Override the target with `CYBERSEC_VAULT` or `CYBERSEC_REMOTE`.

## Agent access (MCP)

Pi connects to this vault two ways:

1. **Direct file access** — `read`/`write`/`bash` against the directory. Always available.
2. **MCP server** — `obsidian-mcp@2` (npm), registered as `obsidian` in `~/.pi/agent/mcp.json`, exposing `obsidian_read_note`, `obsidian_edit_note`, `obsidian_move_note`, `obsidian_search_vault`, tag tools and more.

The MCP path is preferred for edits because it:
- returns an **ETag** per note, so an edit fails with `REVISION_CONFLICT` instead of overwriting changes made in the Obsidian editor;
- wraps writes in a **journaled transaction** with rollback;
- rewrites **backlinks** on rename/move, but only where the target is unambiguous;
- moves deletions to `.obsidian-mcp/trash` rather than deleting.

Recovery (stop the server first):

```bash
npx -y obsidian-mcp@2 recovery list  --vault cybersec=/home/monochrome/Documents/CyberSec
npx -y obsidian-mcp@2 recovery restore --vault cybersec=/home/monochrome/Documents/CyberSec --id <id>
```

`.obsidian-mcp/` holds the transaction journal and trash (30 days, 1 GiB cap by default). It is excluded from search, Linter and the graph via `userIgnoreFilters`.

## Public repository rules

Because the vault is public, ingest must stay generic:

- **Never** file credentials, API keys, tokens, licence keys or password hashes.
- **Never** file real internal hostnames, IP addresses, domains, or customer/employer names.
- **Never** file personal data of any kind (names, emails, phone numbers, ID numbers, addresses).
- **Never** file unverified negative claims about named people or organisations.
- Sanitise screenshots and pasted command output before they enter `_Attachments/`.
- Lab material from real engagements is out of bounds; use the generic pattern instead of the specific target.

If a braindump contains any of the above, Pi should stop, flag it, and ask — not silently generalise it.
