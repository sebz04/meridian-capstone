# Research Wiki Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a Karpathy-pattern research wiki for the Meridian Markets capstone, seeded from the client brief, that accumulates knowledge across 8 weeks.

**Architecture:** Three-layer model — immutable `raw/` sources, Claude-maintained `wiki/` pages, and a `wiki/CLAUDE.md` schema that defines all conventions and workflows. All launch content is seeded from `raw/clinet_brief.md`. Knowledge compounds as new sources are added to `raw/`.

**Tech Stack:** Markdown (GitHub-flavored), git

## Global Constraints

- `raw/` files are never modified after being added — read-only
- `wiki/` files are never edited manually by humans — only by Claude following the schema
- Every wiki page requires frontmatter: `source:` and `last-updated:` (YYYY-MM-DD)
- Page filenames: `kebab-case.md`
- Cross-links between related pages use relative Markdown links
- Spec: `docs/superpowers/specs/2026-09-11-research-wiki-design.md`

---

### Task 1: Scaffold directory structure and write schema

**Files:**
- Create: `wiki/CLAUDE.md`
- Create: `wiki/entities/` (directory)
- Create: `wiki/concepts/` (directory)
- Create: `wiki/analysis/` (directory, with `.gitkeep`)
- Create: `wiki/interview-prep/` (directory)

**Done looks like:** `wiki/CLAUDE.md` defines all three workflows (Ingest, Query, Lint) and all conventions. Four subdirectories exist under `wiki/`.

**How to check:** Run `cat wiki/CLAUDE.md` — verify Ingest, Query, and Lint sections are present. Run `ls wiki/` — verify four subdirectories are listed.

- [ ] **Step 1: Create directory structure**

```bash
mkdir -p wiki/entities wiki/concepts wiki/analysis wiki/interview-prep
touch wiki/analysis/.gitkeep
```

- [ ] **Step 2: Write `wiki/CLAUDE.md`**

```markdown
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
```

- [ ] **Step 3: Verify**

```bash
cat wiki/CLAUDE.md
ls wiki/
```

Expected: CLAUDE.md shows three workflow sections. `ls` shows: `CLAUDE.md  analysis/  concepts/  entities/  interview-prep/`

- [ ] **Step 4: Commit**

```bash
git add wiki/
git commit -m "feat: scaffold wiki directory structure and schema"
```

---

### Task 2: Create index and log

**Files:**
- Create: `wiki/index.md`
- Create: `wiki/log.md`

**Done looks like:** `index.md` has three categories (Stakeholders, Concepts, Interview Prep) with relative links to all pages that will be created in Tasks 3–5. `log.md` has a single dated entry recording the initial ingest.

**How to check:** `cat wiki/index.md` — three categories present, all links listed. `cat wiki/log.md` — one entry with date 2026-09-11, source file, and all pages listed.

- [ ] **Step 1: Write `wiki/index.md`**

```markdown
---
source: raw/clinet_brief.md
last-updated: 2026-09-11
---

# Research Wiki Index

## Stakeholders

- [Dana Okafor](entities/dana-okafor.md) — VP of Operations, Meridian Markets
- [Meridian Markets](entities/meridian-markets.md) — client organization

## Concepts

- [Loyalty Program](concepts/loyalty-program.md)
- [Store Performance](concepts/store-performance.md)
- [Expansion](concepts/expansion.md)

## Interview Prep

- [Interview Questions](interview-prep/questions.md)
- [Team Briefing](interview-prep/briefing.md)
- [Outcomes — What We Must Learn](interview-prep/outcomes.md)
```

- [ ] **Step 2: Write `wiki/log.md`**

```markdown
---
last-updated: 2026-09-11
---

# Wiki Log

Append-only. One entry per ingest operation. Never delete or edit past entries.

---

## 2026-09-11 — Initial ingest

**Source:** `raw/clinet_brief.md`
**Pages created:**
- `wiki/entities/dana-okafor.md`
- `wiki/entities/meridian-markets.md`
- `wiki/concepts/loyalty-program.md` (stub)
- `wiki/concepts/store-performance.md` (stub)
- `wiki/concepts/expansion.md` (stub)
- `wiki/interview-prep/questions.md`
- `wiki/interview-prep/briefing.md`
- `wiki/interview-prep/outcomes.md`
```

- [ ] **Step 3: Verify**

```bash
cat wiki/index.md
cat wiki/log.md
```

Expected: index shows three categories with seven total links. Log shows one entry dated 2026-09-11 listing eight pages.

- [ ] **Step 4: Commit**

```bash
git add wiki/index.md wiki/log.md
git commit -m "feat: add wiki index and log seeded from client brief"
```

---

### Task 3: Create entity pages

**Files:**
- Create: `wiki/entities/dana-okafor.md`
- Create: `wiki/entities/meridian-markets.md`

**Done looks like:** Both pages have correct frontmatter, all fields from the spec, and cross-link to each other. `meridian-markets.md` links to `docs/data-handling-checklist.md`.

**How to check:** `cat wiki/entities/dana-okafor.md` — verify role, communication style, and priorities sections are present. `cat wiki/entities/meridian-markets.md` — verify store count, revenue, data assets table, and checklist link are present.

- [ ] **Step 1: Write `wiki/entities/dana-okafor.md`**

```markdown
---
source: raw/clinet_brief.md
last-updated: 2026-09-11
---

# Dana Okafor

**Role:** VP of Operations, [Meridian Markets](meridian-markets.md)

## Communication

- Email is best; slow to reply Tuesdays and Wednesdays (travel days)
- Has an assistant who can schedule meetings but cannot answer analytics questions
- Direct, informal tone — writes between flights
- Silence does not mean a problem

## Priorities

- Increase revenue
- Reduce operating costs
- Improve customer experience
- Decide on next store location — Pasadena is the leading candidate
- Better use of loyalty program data (~40,000 members; currently underused)

## Decision-making context

Currently makes expansion calls on instinct and spreadsheets. Wants data to
back up the Pasadena decision before committing. Represents leadership's
desire for clearer visibility before the next expansion round.
```

- [ ] **Step 2: Write `wiki/entities/meridian-markets.md`**

```markdown
---
source: raw/clinet_brief.md
last-updated: 2026-09-11
---

# Meridian Markets

**Type:** Specialty grocery chain
**Geography:** Los Angeles, Orange, and Ventura counties
**Stores:** 14 (grew from 6 in five years)
**Revenue:** ~$78M/year
**Employees:** ~620

## Competitive positioning

Competes on prepared foods, local sourcing, and a smaller footprint than
national chains. Expanded by taking over leases from chains that left
neighborhoods considered underserved.

## Growth pattern

Performance across stores is uneven — some found their footing quickly,
others were slower. Leadership wants visibility into which stores and
categories are performing before the next expansion round.

## Data assets

| Dataset | Details |
|---|---|
| POS transactions | ~3 years; migrated to new system last spring |
| Loyalty program | ~40,000 members; purchase history; underused |
| Labor scheduling | Hours and schedules |
| Store attributes | Square footage, opening date, lease terms |

**Data contact:** Marcus (IT) — provides extract once NDA is signed.
**Data handling rules:** See [`docs/data-handling-checklist.md`](../docs/data-handling-checklist.md).

## Key people

- [Dana Okafor](dana-okafor.md) — VP of Operations
```

- [ ] **Step 3: Verify**

```bash
cat wiki/entities/dana-okafor.md
cat wiki/entities/meridian-markets.md
```

Expected: both files show frontmatter, all required sections, and cross-links between them.

- [ ] **Step 4: Commit**

```bash
git add wiki/entities/
git commit -m "feat: add Dana Okafor and Meridian Markets entity pages"
```

---

### Task 4: Create interview prep pages

**Files:**
- Create: `wiki/interview-prep/questions.md`
- Create: `wiki/interview-prep/briefing.md`
- Create: `wiki/interview-prep/outcomes.md`

**Done looks like:** `questions.md` has four topic groups with actual questions (not placeholders). `briefing.md` has "what we know" and "gaps" sections seeded from the brief. `outcomes.md` has a debrief checklist with must-answer, should-answer, and nice-to-have tiers. All three cross-link to each other.

**How to check:** Read each file — no placeholder text, all content drawn from the brief. Check that each file links to the other two.

- [ ] **Step 1: Write `wiki/interview-prep/questions.md`**

```markdown
---
source: raw/clinet_brief.md
last-updated: 2026-09-11
---

# Interview Questions — Dana Okafor

Use alongside [briefing.md](briefing.md) and [outcomes.md](outcomes.md).

## 1. Goals

- What does success look like for this project beyond the dashboard deliverable?
- How are store-level decisions made today — who is in the room, what triggers action?
- What does leadership most want to understand before committing to Pasadena?

## 2. Data & Systems

- What changed with the POS migration last spring — any data gaps or format
  differences we should know about?
- Has the loyalty program data ever been analyzed? What was found, if so?
- Are there known data quality issues in any of the four datasets?
- How complete is the labor scheduling data — any gaps by store or time period?

## 3. Operations

- What distinguishes the stores that took off quickly from the ones that were slower?
- Is there a store you consider the best example of what Meridian wants to be? Why?
- How does labor scheduling relate to store performance — is there a model or ad hoc?

## 4. Expansion

- Why Pasadena specifically — what is the hypothesis?
- What would make leadership say no to Pasadena even if the data looks good?
- What is the timeline for the expansion decision, and who makes the final call?
```

- [ ] **Step 2: Write `wiki/interview-prep/briefing.md`**

```markdown
---
source: raw/clinet_brief.md
last-updated: 2026-09-11
---

# Team Briefing — Meridian Stakeholder Interview

Read before the interview. Use alongside [questions.md](questions.md)
and [outcomes.md](outcomes.md).

## What we know (from the brief)

- 14 stores across LA, Orange, Ventura counties; ~$78M revenue; ~620 employees
- Grew from 6 to 14 stores in 5 years, taking over leases in underserved neighborhoods
- Competes on prepared foods, local sourcing, smaller footprint than national chains
- Store performance is uneven — some fast, some slow to find footing
- Loyalty program has ~40,000 members and has not been meaningfully used
- Four datasets available: POS (~3 years), loyalty, labor, store attributes
- POS migrated to a new system last spring
- Pasadena is the leading candidate for the next location
- Leadership currently makes expansion decisions on instinct and spreadsheets
- Three-week board preview deadline; eight-week full project timeline
- Dana travels Tuesdays and Wednesdays; email is best

## Open questions (not answerable from the brief)

- What specific metrics does leadership use — even informally — to judge store performance?
- What does "prepared foods" and "local sourcing" mean operationally — is it tracked in POS?
- Is pre-migration POS data compatible with post-migration data?
- Has any analysis of the loyalty data ever been attempted, internally or externally?
- What is the board expecting to see in three weeks — format, depth, specific questions?
- Who beyond Dana is a stakeholder in this project?

## Gaps to close in the interview

- Understand what "success" means concretely to Dana and to leadership
- Get clarity on the Pasadena hypothesis — what is the evidence for it?
- Understand the data quality landscape before the extract arrives from Marcus
```

- [ ] **Step 3: Write `wiki/interview-prep/outcomes.md`**

```markdown
---
source: raw/clinet_brief.md
last-updated: 2026-09-11
---

# Interview Outcomes — What We Must Walk Away Knowing

Post-interview debrief checklist. For each item, mark: Got it / Partial / Missed.
Use alongside [questions.md](questions.md) and [briefing.md](briefing.md).

---

## Must-answer

- [ ] What does success look like for this project beyond the dashboard?
- [ ] What is the Pasadena hypothesis — what data would confirm or deny it?
- [ ] Who makes the final expansion decision and what does that process look like?
- [ ] What changed with the POS migration — any compatibility or quality issues?
- [ ] Has the loyalty data ever been used — what do they actually want from it?

## Should-answer

- [ ] What distinguishes high-performing stores from slower ones, in Dana's view?
- [ ] What is the board expecting to see in three weeks?
- [ ] Are there known data quality issues we should anticipate?
- [ ] Who else on Meridian's team will we interact with?

## Nice-to-have

- [ ] Is there a store Dana considers the best model of what Meridian wants to be?
- [ ] What would make leadership say no to Pasadena despite good data?
- [ ] What does "prepared foods" and "local sourcing" mean in the POS — is it a category?
```

- [ ] **Step 4: Verify**

```bash
cat wiki/interview-prep/questions.md
cat wiki/interview-prep/briefing.md
cat wiki/interview-prep/outcomes.md
```

Expected: all three files contain seeded content with no placeholder text, and each links to the other two.

- [ ] **Step 5: Commit**

```bash
git add wiki/interview-prep/
git commit -m "feat: add interview prep pages — questions, briefing, outcomes"
```

---

### Task 5: Create concept stubs [x] complete — see .superpowers/sdd/progress.md

**Files:**
- Create: `wiki/concepts/loyalty-program.md`
- Create: `wiki/concepts/store-performance.md`
- Create: `wiki/concepts/expansion.md`

**Done looks like:** Three stub files exist with correct frontmatter, a clearly marked stub status line, what is known from the brief, open questions to answer as research grows, and cross-links to related pages.

**How to check:** `ls wiki/concepts/` shows three files. `cat` each — verify frontmatter is present, "Status: Stub" line is there, and at least two cross-links exist per file.

- [ ] **Step 1: Write `wiki/concepts/loyalty-program.md`**

```markdown
---
source: raw/clinet_brief.md
last-updated: 2026-09-11
---

# Loyalty Program

**Status:** Stub — expand as sources arrive.

## Known (from brief)

- ~40,000 members
- Purchase history available
- Has not been meaningfully analyzed by Meridian to date
- Dana identifies this as an underused asset

## Open questions

- What data is captured per transaction — amount only, or also items and categories?
- What is the enrollment rate relative to total customer volume?
- Is there any segmentation or tier structure in the program?
- What would "using the loyalty data" actually look like for Dana's team?

## Related

- [Meridian Markets](../entities/meridian-markets.md)
- [Store Performance](store-performance.md)
```

- [ ] **Step 2: Write `wiki/concepts/store-performance.md`**

```markdown
---
source: raw/clinet_brief.md
last-updated: 2026-09-11
---

# Store Performance

**Status:** Stub — expand as sources arrive.

## Known (from brief)

- 14 stores; performance is uneven — some took off quickly, others were slower
- Leadership currently judges performance on instinct and spreadsheets
- Dashboard goal: sales performance by store and by category

## Open questions

- What metrics does Meridian currently track per store, formally or informally?
- What is the revenue spread across stores — which are top and bottom performers?
- Is there a correlation between store age, square footage, neighborhood type, and performance?
- How is "category" defined in the POS — what categories exist?

## Related

- [Meridian Markets](../entities/meridian-markets.md)
- [Expansion](expansion.md)
- [Loyalty Program](loyalty-program.md)
```

- [ ] **Step 3: Write `wiki/concepts/expansion.md`**

```markdown
---
source: raw/clinet_brief.md
last-updated: 2026-09-11
---

# Expansion

**Status:** Stub — expand as sources arrive.

## Known (from brief)

- Pasadena is the leading candidate for the next location
- Leadership wants data to back up the decision before committing
- Past expansion: took over leases from chains leaving underserved neighborhoods
- Growth pattern: 6 to 14 stores in 5 years

## Open questions

- What criteria drove past site selections — lease availability, demographics, proximity?
- What is the Pasadena hypothesis specifically — what makes it attractive?
- Which existing store is most comparable to the proposed Pasadena market, and how did it perform?
- What is the timeline for the board decision?

## Related

- [Store Performance](store-performance.md)
- [Meridian Markets](../entities/meridian-markets.md)
- [Dana Okafor](../entities/dana-okafor.md)
```

- [ ] **Step 4: Verify**

```bash
ls wiki/concepts/
cat wiki/concepts/expansion.md
```

Expected: three files listed. `expansion.md` shows frontmatter, Status line, Known section, Open questions, and three cross-links.

- [ ] **Step 5: Commit**

```bash
git add wiki/concepts/
git commit -m "feat: add concept stubs — loyalty program, store performance, expansion"
```
