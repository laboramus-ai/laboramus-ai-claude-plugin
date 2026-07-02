---
description: Builds a reusable candidate profile from the user's CV, work certificates, and diplomas (and optionally personality tests). Use when the user uploads career documents or asks to build/update their profile. Produces a candidate-profile.md reused across all applications.
---

# Laboramus — Build Profile

Extract a reusable candidate profile from the user's documents. Built ONCE, reused for every application (the CV is not re-analyzed each time). Output: `profile/candidate-profile.md`.

## Inputs
Read every document in `profile/source-documents/`:
- `cv/`, `work-certificates/`, `diplomas/` — the factual basis.
- `personality-tests/` — OPTIONAL. Most users have none; the profile must be fully valuable without it.

## Language of mixed-language sources
Source documents may be in different languages (CV German, diploma English, certificate French). Write the **profile in the user's language**. Keep proper nouns and skill/technology names as-is (Python, Kubernetes, company names, certifications).

## What to extract → `candidate-profile.md`
A readable Markdown document:

### Summary
2–3 sentences: who this candidate is professionally.

### Hard skills
For each: `Skill — Level (Beginner/Professional/Senior/Expert/Senior Expert), N+ years, context`. The level + years signal matters — preserve it. Base levels on real evidence (years, seniority of roles), don't inflate.

### Soft skills
For each: skill + evidence (quote from a work certificate where possible).

### Experience
Each role: title · company · dates · key responsibilities/achievements (with numbers if present).

### Education & certifications
Degrees, diplomas, certifications with institutions and years.

### Languages

### Personality (only if personality-tests/ has usable results)
Summarize as descriptive strengths, work style, values, motivation — what the test *states*. Do NOT match it to any role here. If no usable test, omit this section entirely. (A test that's just a CV/other doc → say so, don't invent.)

## Stale-skill flagging
If a skill's last evidenced use is long ago (e.g. "last used 2012"), add a gentle inline flag: `⚠️ last evidenced 2012 — still current?`. You CANNOT know the user's intent (maybe they're moving away from it), so flag, don't delete.

## User control
Tell the user this file is **theirs to edit**: they can delete skills they don't want to present, annotate, or correct anything. The file is the editable source of truth — no hidden settings.

## No invention
Only what's in the documents. No invented numbers, employers, technologies, or achievements.
