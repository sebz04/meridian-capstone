---
name: research-wiki-design
description: Design spec for the Meridian Markets research wiki, following the Karpathy LLM wiki pattern
metadata:
  type: project
---

# Design Spec: Meridian Markets Research Wiki

**Date:** 2026-09-11
**Project:** Meridian Markets capstone
**Pattern:** Karpathy LLM wiki (https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)

---

## Purpose

A persistent, Claude-maintained research wiki that accumulates knowledge across the full 8-week capstone project. Starts with interview prep for the Dana Okafor stakeholder meeting; grows as new sources (internal documents, industry research, academic references) are added to `raw/`.

The core problem it solves: without a wiki, Claude rediscovers context from scratch each session. With it, knowledge compounds.

---

## Audience

- LMU MSBA workshop team (primary users — read wiki, add raw sources, direct Claude)
- Claude (maintains all wiki content automatically per schema)

---

## Repository Structure

```
raw/                              ← immutable source documents (read-only)
  clinet_brief.md                 ← first source
  [future: emails, PDFs, articles, data dictionaries]

wiki/                             ← Claude-maintained (humans read, Claude writes)
  CLAUDE.md                       ← schema: structure, conventions, workflows
  index.md                        ← content catalog organized by category
  log.md                          ← append-only ingest history
  entities/
    dana-okafor.md
    meridian-markets.md
  concepts/                       ← stubbed at launch, filled as sources arrive
    loyalty-program.md
    store-performance.md
    expansion.md
  analysis/                       ← comparisons, syntheses, derived insights
  interview-prep/
    questions.md
    briefing.md
    outcomes.md
```

---

## Three-Layer Model

| Layer | Location | Owner | Rule |
|---|---|---|---|
| Raw sources | `raw/` | Team | Never modified after added |
| Wiki pages | `wiki/` | Claude | Never edited manually by humans |
| Schema | `wiki/CLAUDE.md` | Team | Defines all conventions and workflows |

---

## Launch Content (seeded from `clinet_brief.md`)

### `wiki/index.md`
Content catalog with two categories at launch: *Stakeholders* and *Interview Prep*. A new category is added each time a page type that doesn't fit existing categories is created.

### `wiki/log.md`
Append-only. First entry: date, source file ingested, pages created or updated. One entry per ingest operation.

### `wiki/entities/dana-okafor.md`
- Role: VP of Operations, Meridian Markets
- Communication: email-first, travels Tue/Wed, slow to reply those days, direct tone
- Priorities: revenue growth, cost reduction, customer experience, next location decision (Pasadena)
- Source: `raw/clinet_brief.md`

### `wiki/entities/meridian-markets.md`
- 14 stores across LA, Orange, Ventura counties
- ~$78M annual revenue, ~620 employees
- Grew from 6 to 14 stores in 5 years by taking over leases in underserved neighborhoods
- Competes on prepared foods, local sourcing, smaller footprint
- Data assets: POS (~3 years), loyalty (~40K members), labor schedules, store attributes
- NDA constraints: see `docs/data-handling-checklist.md`
- Source: `raw/clinet_brief.md`

### `wiki/interview-prep/questions.md`
Prioritized questions in four groups:
1. **Goals** — what does success look like beyond the dashboard; how are decisions made today
2. **Data & systems** — POS migration details; loyalty program usage history; known data quality issues
3. **Operations** — what distinguishes high-performing stores from slower ones; labor model
4. **Expansion** — why Pasadena; what would make leadership say no; timeline and constraints

### `wiki/interview-prep/briefing.md`
- What the team knows going in (from the brief)
- Open questions not answerable from the brief
- Gaps to close before or during the interview

### `wiki/interview-prep/outcomes.md`
- What the team must walk away knowing after the interview
- Used as a debrief checklist: did we get answers, partial answers, or nothing on each item

### Concept stubs (filled as sources arrive)
- `wiki/concepts/loyalty-program.md`
- `wiki/concepts/store-performance.md`
- `wiki/concepts/expansion.md`

---

## Schema (`wiki/CLAUDE.md`) — Workflows

### Ingest
Triggered when a new file is added to `raw/`:
1. Read the source
2. Discuss key takeaways with the team
3. Write or update the relevant wiki page(s)
4. Append an entry to `log.md`
5. Update `index.md`

### Query
Triggered when the team asks a research question:
1. Read relevant wiki pages
2. Synthesize an answer
3. If the answer is valuable and not already captured, file it into the appropriate wiki page

### Lint
Triggered on request:
1. Flag contradictions between pages
2. Identify stale claims
3. Surface orphan pages missing from `index.md`
4. Note missing cross-links between related pages

---

## Conventions (enforced by schema)

- Page filenames: `kebab-case.md`
- Required frontmatter on every wiki page: `source:` (which raw file(s) it draws from) and `last-updated:` (date)
- `raw/` files are never modified after being added
- `wiki/` files are never edited manually by humans — only by Claude following the schema
- Cross-links between related pages use relative Markdown links

---

## Source Types Supported

| Type | Examples |
|---|---|
| Internal / client | Brief, emails from Dana, data dictionaries, extract documentation |
| Industry research | Specialty grocery market reports, LA demographic data, competitor analysis |
| Academic / methods | Analytics frameworks, dashboard design literature, loyalty program research |
