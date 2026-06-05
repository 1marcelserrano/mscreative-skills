# Cowork Setup — Reference Templates

These are starter templates for core files. Adapt to each user — never use as-is.

---

## about-me.md — Starter Template

```markdown
# About Me

## Who I Am
[Name], [Role] at [Company/Context]. [One sentence about what the company does.]

## What I Do
[2-3 sentences about actual day-to-day work. Not a LinkedIn headline — what you spend hours doing.]

## Current Priorities
- [Priority 1 — what matters this quarter]
- [Priority 2]
- [Priority 3]

## How I Communicate
- Tone: [formal / casual-professional / casual]
- Length: [concise / detailed / depends on context]
- I like: [data, examples, directness, humor — be specific]
- I dislike: [fluff, jargon, hedging, over-explanation — be specific]

## My Voice — Example
[Paste 2-3 sentences from something they actually wrote. This is the single most impactful part for voice matching.]
```

**Constraint:** Maximum 300 words. Every word costs tokens on every task.

---

## writing-style.md — Starter Template

```markdown
# Writing Style Rules

## Words I Never Use
delve, leverage, utilize, harness, navigate, landscape, robust, seamless,
cutting-edge, game-changer, unlock, empower, holistic, synergy, deep dive,
in today's fast-paced world, it's important to note, at the end of the day,
as a matter of fact, needless to say

## Voice Rules
- [Active voice / passive allowed?]
- [Short sentences / long ok?]
- [First person / third person / depends?]
- [Contractions yes/no?]
- [Humor yes/no?]

## Formatting Rules
- [Headers: use them / avoid them / only for long docs]
- [Bullet points: yes / prefer prose / only for lists]
- [Emoji: never / sparingly / yes]
- [Bold: for emphasis / avoid]

## What Good Looks Like
"[A sentence or two showing the target tone and style.]"

## What Bad Looks Like
"[A sentence showing generic AI output they want to avoid.]"
```

**Constraint:** Maximum 200 words. This file is read before every writing task.

---

## KNOWLEDGE/_INDEX.md — Starter Template

```markdown
# KNOWLEDGE — INDEX

> Entry point for the accumulated knowledge system.
> Read top-down. Only load specific files when needed.

---

## DOMAIN (what things are)

| File | Scope |
|------|-------|
| *(No domain files yet — created as knowledge emerges)* | |

## PROCEDURAL (how to do things)

| File | Scope |
|------|-------|
| *(No procedural files yet — created as patterns emerge)* | |

## ERRORS

| File | Scope |
|------|-------|
| ERRORS.md | Classified error log — deterministic, infrastructure, resolved |

---

> New categories are created as patterns emerge.
> Merge when categories overlap. Split when files exceed 200 lines.
```

**Constraint:** Keep this file as a routing table, not a knowledge store. It tells Claude where to look, not what to know.

---

## KNOWLEDGE/ERRORS.md — Starter Template

```markdown
# ERRORS — CLASSIFIED LOG

> Not every error is a conclusion. Classify before acting.
> Mature conclusions graduate to the relevant domain or procedural file.

---

## Classification

- **DET** = Deterministic (bad schema, wrong type, missing field) → conclude immediately
- **INF** = Infrastructure (timeout, rate limit, network) → log, no conclusion until pattern emerges
- **RES** = Resolved → graduated to relevant file

---

## Log

| Date | Type | Context | Description | Status |
|------|------|---------|-------------|--------|
| — | — | — | No errors logged yet | — |

---

> When an INF entry repeats 3+ times → promote to conclusion and migrate.
> When a DET entry is fixed → mark RES and note the correction.
```

**Constraint:** This is a living log, not a historical archive. Prune resolved entries periodically.

---

## CLAUDE.md — Starter Template (Global Instructions)

```markdown
# GLOBAL INSTRUCTIONS

## BEFORE EVERY TASK

1. Read ABOUT_ME/ — no task starts without reading about-me.md and writing-style.md.
2. Review KNOWLEDGE/_INDEX.md — load relevant knowledge for the task.
3. If the task relates to a project, read the matching PROJECTS/ subfolder first.
4. If the task involves a content type with a matching TEMPLATES/ pattern, study that template's structure. Use the structure, not the content.

## FOLDER PROTOCOL

Three read-only folders. Two write folders.

### Read-only — never create, edit, or delete here:
- ABOUT_ME/ — Identity and writing rules.
- TEMPLATES/ — Proven structures to reuse.
- PROJECTS/ — Briefs, references, deliverables by project.

### Write folders:
- KNOWLEDGE/ — Accumulated knowledge between sessions. Claude reads and writes freely.
- CLAUDE_OUTPUTS/ — All finished work. Mirror PROJECTS/ structure.

## NAMING CONVENTION

Format: PROJECT_CONTENT-TYPE_V1.ext
Examples: ACME_REPORT_V1.md, Q4_NEWSLETTER_V1.docx
Increment version if file exists. Never overwrite.
Exception: Knowledge files are living documents — no versioning needed.

## LEARNING

Track two types of knowledge in KNOWLEDGE/:
- Domain (what things are): preferences, project decisions, business rules, naming conventions.
- Procedural (how to do things): deploy steps, review flows, publication protocols.

Log errors to KNOWLEDGE/ERRORS.md. Classify before acting:
- Deterministic → conclude immediately.
- Infrastructure → log, wait for pattern.
- Resolved → graduate to the relevant domain or procedural file.

Actively maintain:
- Review at session start. Merge overlaps. Split >200 lines. Prune stale knowledge.
- Propose edits to CLAUDE.md when patterns emerge — don't wait to be asked.

## OPERATING RULES

- If the brief is unclear, use AskUserQuestion. Don't fill gaps with filler.
- Deliver the work. Save commentary unless asked.
- Never delete files anywhere.
- Before delivering final output, verify it matches about-me.md voice and writing-style.md rules.
```

**Constraint:** Maximum 150 lines. Shorter = more reliable compliance.

---

## .claude/rules/ — Project-Specific Rule Template

```yaml
# .claude/rules/[client-name].md
---
paths:
  - "PROJECTS/[ClientName]/**"
---
When working on [Client] deliverables:
- [Language/tone rule]
- [Required sections or format]
- [Brand reference file location]
```

Use only for users with 3+ active projects needing different rules per project.

---

## Universal Prompt Template

```
I want to [TASK] for [SUCCESS CRITERIA].

First, explore my folder. Then, ask me questions using
AskUserQuestion. Refine the approach with me before executing.
```

### Use Case Variations

**Writing content:**
```
I want to write my next newsletter on [topic] with [angle/hook].

First, explore my folder. Then, ask me questions using
AskUserQuestion. Refine the approach with me before executing.
```

**Consulting deliverable:**
```
A client just sent a brief for [project]. The brief is in PROJECTS/[client]/.

Read the brief, my deliverable template, and my past examples.
Create a first draft as a .docx. Ask me questions first (AskUserQuestion).
```

**Research and analysis:**
```
I uploaded [N] articles/reports about [topic]. Read all of them.
Create a comparison table: what each one covered, what they missed,
and where I can say something new. Ask me questions first.
```

**Recurring automation (with /schedule plugin):**
```
Every Monday at 7am, research [competitor names] for news, product updates,
or pricing changes. Save a summary to CLAUDE_OUTPUTS/weekly-briefings/ as markdown.
Only include items from the past 7 days.
```

---

## Context Hygiene Quick Reference

| Element | Max Size | Why |
|---|---|---|
| about-me.md | 300 words | Read every task. Bloat = wasted tokens. |
| writing-style.md | 200 words | Frequently referenced. Keep surgical. |
| CLAUDE.md | 150 lines | Shorter = higher compliance rate. |
| ABOUT_ME/ folder total | 1,000 words | Everything here is loaded often. |
| KNOWLEDGE/ per file | 200 lines max | Split when it grows beyond this. |
| Single PROJECTS/ subfolder | Extract, don't dump | 50-page PDF → 1-page brief. |

**Session discipline:**
- `/clear` between unrelated tasks
- One complex task per session
- Review every output before sharing
