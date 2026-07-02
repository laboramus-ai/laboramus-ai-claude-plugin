---
description: Orchestrates a job application end to end. Use when the user wants to apply for a job, analyze a posting/company, or work on an application. Resolves whatever input the user has (job URL, company URL, or pasted text), runs every analysis step whose inputs are satisfied, and reports what's still missing. The single entry point for the Laboramus workflow.
---

# Laboramus — Apply (Orchestrator)

The main entry point. Figure out what the user has, run what can be run, tell them what's missing. One skill steers everything; the individual skills below can also be called directly by advanced users.

## Step 0 — Workspace
If a `Laboramus/` workspace doesn't exist yet in the project, run the **init** skill first (scaffold folders). If no `profile/candidate-profile.md` exists, mention that building a profile (build-profile skill) unlocks the personal fit comparison and the cover letter — but don't force it; employer + role analysis work without it.

## Step 1 — Resolve the input (input path ≠ skill)
Ask "What do you have?" and handle whichever applies:
- **(a) a job-posting URL** (portal / LinkedIn / company site): try to read it; identify the company from it.
- **(b) a company + URL**: company only.
- **(c) a role + URL**: read the posting; derive company if possible.
- **(d) pasted job text**: use directly.

Normalize everything to `{ company (name/URL, optional), job-posting text }`.

**If a URL can't be read** (LinkedIn and many JS-heavy/auth-walled sites fail): say so plainly and ask the user to paste the text. The paste path is the reliable fallback. Optionally offer the Claude-for-Chrome route (see analyze-employer) for pages behind a login.

## Step 2 — Create / locate the application folder
Application folder: `applications/<YYYY-MM-DD>-<company-slug>-<role-slug>/` (slugify: lowercase, spaces→`-`, strip special chars, cap role slug ~40 chars). Propose the name, let the user override. Save the pretty display name (e.g. "Acme — Senior Software Architect, Jun 2026") into `status.json`. Write `job-posting.md` and `company.md`.

## Step 3 — Run what's runnable, in dependency order
- **analyze-employer** — if a company is known. (Reuses a cached `companies/<slug>/employer.md` if present — see that skill.)
- **analyze-role** — if a posting is present. Needs no profile.
- **compare-fit** — only if BOTH role-requirements AND a candidate profile exist. Otherwise tell the user: "Upload a CV / build your profile to unlock the fit comparison."
- **cover-letter** — offer once a profile + posting exist (it can short-circuit missing analyses).
- **interview-prep** — offer after a letter/brief exists.

After each step, update `status.json` (which steps done, fitScore if available, dates). Report progress and what's still missing in the user's language.

## Step 4 — Navigation
Offer to build/refresh the **dashboard** (Live Artifact) so the user can see all applications, statuses, and fit scores in one place.

## Language (two domains — always)
- Cover letter → the **job-posting's** language.
- Everything the user reads (analyses, brief, this conversation) → the **user's** language (chat language; ask if unclear).
