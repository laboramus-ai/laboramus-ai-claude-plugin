---
description: Builds or refreshes a dashboard showing all applications, their status, progress, fit scores, and latest contact. Use when the user wants an overview of their applications or to navigate between them.
---

# Laboramus — Dashboard

Give the user one place to see everything. **Primary form: a self-contained `dashboard.html`** written into the `Laboramus/` root — regenerated from the files on every run ("refresh the dashboard" = re-read the sources, rewrite the file). Present the file to the user after writing it.

## Data sources (read the whole workspace)
`status.json` fields are defined in `../../references/status-schema.md` — parse exactly those.
- `profile/candidate-profile.md` → profile status (built? how many skills? last updated).
- `applications/*/status.json` → display name, `applicationStatus` (preparing/applied/interview/offer/rejected/withdrawn), `steps` done, `fitScore`, dates.
- `applications/*/notes.md` → latest contact date + next step.
- `companies/*/` → which companies have cached analyses.

## What to render
A single page:
- **Profile** card: status + last update.
- **Applications** table: display name · company · **applicationStatus** (color-coded) · fit score · progress row (employer ✓/—, role ✓/—, fit ✓/—, letter ✓/—, interview ✓/—) · latest contact + next step from notes.
- Sort by `updatedAt` (newest first); show fit score and status prominently.
- Per application, list the file names of its artifacts (analyses, strategy brief, cover letter, interview prep, notes) so the user knows what exists and where.

Self-contained HTML: inline CSS, no external scripts, no network calls — it must render offline from the file system.

## Optional: Live Artifact
If the environment supports creating a persistent Artifact (Cowork sidebar), you MAY additionally offer one. Note honestly: an Artifact cannot read local workspace files by itself — refreshing means regenerating it. The `dashboard.html` on disk remains the source of truth.

## Language
Labels and any descriptive text in the **user's language**.
