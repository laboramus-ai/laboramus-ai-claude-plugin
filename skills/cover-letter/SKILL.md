---
description: Generates a tailored cover letter in two steps — a reviewable strategy brief, then the final letter. Use when the user wants a cover letter / motivation letter for a specific job. Works standalone (derives what it needs) or uses existing analyses.
---

# Laboramus — Cover Letter

Produce a tailored cover letter via two stages, using two sub-agents. The letter is written in the **job posting's language**; the brief and your conversation are in the **user's language**.

## Prerequisites
- Locate the current application folder per `../../references/conventions.md` §1.
- `job-posting.md` and `profile/candidate-profile.md` must exist. If the profile is missing, stop and ask the user to build it (build-profile).
- Existing `analyses/` (employer, role-requirements, fit-comparison) are used if present, but are NOT required — the strategist short-circuits and derives what it needs from the posting + profile.

## Step A — Strategy brief (review gate)
Dispatch the **strategist** sub-agent. It writes `strategy-brief.md` (candidate facts, top 5–7 arguments, tone, three-part narrative, major gaps, personality only-if-it-helps) and stops.

Then SHOW the brief to the user and pause: "Review and correct anything — facts, emphasis, tone. The letter will be in <posting language>. Say 'write the letter' when ready." Let the user edit `strategy-brief.md` or tell you changes. This is the human checkpoint — do not skip it.

## Step B — Write
Once the user approves, dispatch the **writer** sub-agent. It reads the (possibly edited) `strategy-brief.md` and writes `cover-letter.md`: plain text, 300–350 words, three-part structure, banned-word list enforced for the posting's language, no repetition, strong opening hook.

## After
- Show the letter. Offer revisions (the user can ask for tone tweaks, shortening, different emphasis — re-run the writer).
- Update `status.json`: `steps.coverLetter`, `updatedAt` — per `../../references/status-schema.md`.
- Offer interview-prep as a natural next step.

## Standalone use
If the user jumps straight to "write me a cover letter for this job" with only a posting + profile, run A then B directly — the strategist handles the missing analyses. Offer to run the full employer/role/fit analyses too if they want richer results.
