# Pi instructions — CyberSec vault

You are maintaining a personal cyber-security wiki. The owner is a cyber-security graduate; assume degree-level literacy and skip "what is a computer" explanations. Depth over hand-holding, but define acronyms on first use.

## Ingest procedure

When asked to ingest `Unorganised/`:

1. **Read every file** in `Unorganised/` (including subfolders, `.md`, `.txt`, `.html` clippings).
2. **Extract atomic claims**, not prose. One concept = one note.
3. **Search before writing.** `rg -l "<term>"` and check `11 Reference/Glossary.md` plus the relevant `* MOC.md`. Merging into an existing note beats creating a near-duplicate.
4. **Print a filing plan** as a table: source → action (new / merge / skip-duplicate) → target note → top 3 links it will add. Wait for approval unless told "just do it".
5. **Write notes** using `_Templates/Note.md`: frontmatter (`title`, `aliases`, `category`, `tags`, `status`, `created`, `updated`, `sources`), `## Summary`, body sections, `## Related`.
6. **Link both ways**: add `[[New Note]]` to the target section MOC, and add siblings to `## Related`. Never leave an orphan.
7. **Update the glossary** for every new term with a one-line definition.
8. **Archive the source**: `git mv`/`mv` into `_Archive/`, prepend `ingested: 2026-10-23` and the list of notes it produced. Never delete a source.
9. **Report**: notes created, notes merged, links added, anything ambiguous you guessed at.

## Hard rules

- Filenames are Title Case, globally unique. Disambiguate with parentheses, never suffixes like `-2`.
- One concept per file. Split before you bloat.
- Every note links to its section MOC and to ≥3 siblings.
- Never invent facts. If a braindump is ambiguous or wrong, write it down as `> [!warning] Unverified` and flag it in the report rather than silently "fixing" it.
- Never delete content. Supersede it: keep the old text under `## Deprecated` and link the replacement.
- Don't restructure folders without asking.
- `status` must be honest: don't mark a two-line note `solid`.

## When adding new sections

Only when ≥8 notes clearly do not fit an existing folder. Ask first, then: new folder, `<Section> MOC` note, row in `Home.md`, row in `README.md` layout block.

## Style

- `[[Wikilinks]]` for everything, `[[Target|display text]]` when grammar needs it.
- Tables for comparisons, Mermaid for flows, numbered lists for procedures.
- Attack notes use: Summary → How it works → Variants → Detection → Mitigation → Related.
- Actor notes use: Summary → Motivation → Capability → Typical TTPs → Defensive focus → Related.
