# Data Handling Checklist — Meridian Markets Capstone

**Project:** Meridian Markets store performance analysis  
**Client:** Dana Okafor, VP of Operations, Meridian Markets  
**Audience:** LMU MSBA workshop team and Meridian Markets  
**NDA:** Required before any data is requested or received. All handling below is subject to NDA terms.

Work through this checklist once, when the data extract arrives from Marcus (IT). Check off each item as you complete it.

---

## 1. Before You Request the Data

- [ ] Confirm the NDA is fully signed by all team members before contacting Marcus
- [ ] Agree on a single shared storage location (e.g., encrypted shared folder) before the extract is sent
- [ ] Designate one team member as the data contact with Marcus

---

## 2. Receiving the Extract

- [ ] Log the receipt date and a file inventory: dataset name, file format, and approximate row count
- [ ] Confirm all four datasets are present:
  - [ ] POS transactions (~3 years)
  - [ ] Loyalty program membership and purchase history (~40,000 members)
  - [ ] Labor scheduling and hours
  - [ ] Store attributes (square footage, opening date, lease terms)
- [ ] Do not forward the extract over personal email or personal cloud accounts

---

## 3. Storage and Access

- [ ] Store all files only in the agreed shared location — no copies to personal laptops or personal cloud storage
- [ ] Confirm access is limited to team members only
- [ ] Keep raw files intact and unmodified; work only from copies

---

## 4. AI Tool Boundaries

Per the client NDA, **customer records and employee data must not be entered into ChatGPT, Claude, Copilot, or any other AI tool.** This is non-negotiable.

| Dataset | AI tools allowed? |
|---|---|
| POS sales totals by store and week | Yes |
| Store attributes | Yes |
| Loyalty program membership and purchase history | **No** |
| Labor schedules and employee hours | **No** |

- [ ] Every team member has read and understood the rule above before beginning any analysis

---

## 5. During Analysis

- [ ] Before sharing any notebook, slide, screenshot, or output outside the team, verify it contains no loyalty or labor data
- [ ] Do not include loyalty or labor data in deliverables, emails, or presentations shared with anyone outside Meridian Markets
- [ ] If unsure whether something is restricted, treat it as restricted and check with the team contact

---

## 6. End of Project

- [ ] Delete all local and shared copies of the raw data extract upon project completion
- [ ] Confirm deletion with the full team and log the date below

**Deletion confirmed:** _________________________ (date) by _________________________ (name)
