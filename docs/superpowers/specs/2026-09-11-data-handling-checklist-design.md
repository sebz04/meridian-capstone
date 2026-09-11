---
name: data-handling-checklist-design
description: Design spec for the Meridian Markets data handling checklist
metadata:
  type: project
---

# Design Spec: Data Handling Checklist

**Date:** 2026-09-11  
**Project:** Meridian Markets capstone  
**Output file:** `docs/data-handling-checklist.md`

## Purpose

A one-time onboarding checklist for the LMU MSBA workshop team and Meridian Markets. Team members work through it when the data extract arrives from Marcus (IT). Dana and her team can read it as a process overview showing responsible data handling.

## Audience

- LMU MSBA student workshop team (primary users)
- Meridian Markets / Dana Okafor's team (oversight readers)

## Format

Single Markdown file with GitHub-flavored checkboxes. No sign-off block (NDA covers formal acknowledgment). No separate board-preview section (generic rules apply).

## Structure

Six sequential phases:

1. Before you request the data — NDA confirmation, storage agreement, data contact
2. Receiving the extract — log receipt, verify all four datasets
3. Storage and access — agreed location only, no personal copies, raw files intact
4. AI tool boundaries — explicit per-dataset table; honor-system enforcement
5. During analysis — scrub restricted data from outputs before sharing
6. End of project — deletion confirmation with date and name

## Key constraint

Client NDA prohibits loyalty program and labor data from entering any AI tool (ChatGPT, Claude, Copilot, etc.). POS sales totals by store/week and store attributes are explicitly permitted.
