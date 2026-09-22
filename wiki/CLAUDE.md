# Meridian Markets Research Wiki — Schema

This file defines the structure, conventions, and workflows for this wiki.
Claude reads and follows this schema in every session.
Humans read this wiki; Claude maintains it. Never edit wiki pages manually.

---

## Directory Structure

```
raw/                  ← immutable source documents (never modify)
wiki/
  CLAUDE.md           ← this file
  index.md            ← content catalog by category
  log.md              ← append-only ingest history
  entities/           ← people and organizations
  concepts/           ← topics, methods, frameworks
  analysis/           ← comparisons, syntheses, derived insights
  interview-prep/     ← prep materials for stakeholder meetings
```

---

## Conventions

- Filenames: `kebab-case.md`
- Every wiki page must include frontmatter:
  - `source:` — which raw file(s) the page draws from
  - `last-updated:` — date last modified (YYYY-MM-DD)
- This file (`CLAUDE.md`) is the schema itself, not a content page — it is
  exempt from the frontmatter requirement above
- Cross-links between related pages use relative Markdown links
- `raw/` files are never modified after being added
- `wiki/` files are never edited manually — only by Claude
- `raw/clinet_brief.md` is spelled exactly that way (typo for "client") and
  is intentionally left uncorrected — renaming it would modify an immutable
  raw file and break every page's `source:` reference to it. Do not rename
  it.

---

## Data Handling

This repository is public. Before anything derived from the Meridian data
extract enters `raw/` or `wiki/`, check it against
[`../docs/data-handling-checklist.md`](../docs/data-handling-checklist.md).

**Per the client NDA, loyalty program data and labor/employee data must
never be read by an AI tool, summarized into a wiki page, or committed to
this repository — not even as an excerpt.** POS sales totals and store
attributes are the only extract datasets cleared for AI tools and for
`wiki/`. See the checklist's Section 4 for the full table.

---

## Workflow: Ingest

Triggered when a new file is added to `raw/`.

0. If the source is loyalty program data or labor/employee data (or any
   excerpt of either), **stop** — do not read, summarize, or commit it. See
   Data Handling above.
1. Read the source file
2. Discuss key takeaways with the team
3. Write or update the relevant wiki page(s) in `wiki/`
4. Append an entry to `wiki/log.md`
5. Update `wiki/index.md`

---

## Workflow: Query

Triggered when the team asks a research question.

1. Read relevant wiki pages
2. Synthesize an answer
3. If the answer is valuable and not already captured, file it into the
   appropriate wiki page and update `log.md`

---

## Workflow: Lint

Triggered on request ("lint the wiki").

1. Flag contradictions between pages
2. Identify stale claims (source changed, page didn't)
3. Surface orphan pages missing from `index.md`
4. Note missing cross-links between related pages
5. Report findings — do not auto-fix without confirmation
