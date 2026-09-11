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
- Cross-links between related pages use relative Markdown links
- `raw/` files are never modified after being added
- `wiki/` files are never edited manually — only by Claude

---

## Workflow: Ingest

Triggered when a new file is added to `raw/`.

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
