---
description: Builds or refreshes an interactive dashboard showing all applications, their progress, fit scores, and latest contact. Use when the user wants an overview of their applications or to navigate between them. Renders as a Live Artifact in Cowork.
---

# Laboramus — Dashboard

Give the user one place to see and navigate everything. Built as a **Live Artifact** (a persistent, interactive HTML page in Cowork's sidebar that reads local files, so it reflects the current state).

## Data sources (read the whole workspace)
- `profile/candidate-profile.md` → profile status (built? how many skills? last updated).
- `applications/*/status.json` → per application: display name, which steps are done (employer / role / fit / letter / interview), fit score, dates.
- `applications/*/notes.md` → latest contact date + next step.
- `companies/*/` → which companies have cached analyses.

## What to render
A single dashboard with:
- **Profile** card: status + last update.
- **Applications** list/table: display name · company · fit score · a progress row (employer ✓/—, role ✓/—, fit ✓/—, letter ✓/—, interview ✓/—) · latest contact + next step from notes.
- **Drill-down**: clicking an application surfaces its artifacts (analyses, strategy brief, cover letter, interview prep, notes).
- Sort applications by date (newest first); show fit score prominently.

## How to build it
Ask Claude (Cowork) to create this as a **Live Artifact** so it persists in the sidebar and refreshes from the local files. Build the HTML from the data sources above. On a later run, refresh it (re-read the files, update the view).

> ⚠️ Verify at first use: programmatic creation/refresh of a Live Artifact from a skill is the one piece not yet confirmed in docs. If it isn't possible, fall back to writing a `dashboard.html` (or `dashboard.md`) into the `Laboramus/` root that the user opens directly, and tell the user that's what you did.

## Language
Labels and any descriptive text in the **user's language**.
