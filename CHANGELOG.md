# Changelog

## 0.4.0 — 2026-07-03

Added marketplace configuration for direct distribution.

- **Marketplace Distribution Configuration**: Created `.claude-plugin/marketplace.json` to publish the plugin.
- **LICENSE**: Added MIT License to the repository root.
- **Consistent Versioning**: Updated README and documentation to version `0.4.0`.

## 0.2.0 — 2026-07-02

Structural hardening after the first design review.

- **`status.json` now has a defined schema** (`references/status-schema.md`): fixed field names, an `applicationStatus` lifecycle (preparing → applied → interview → offer/rejected/withdrawn), per-step completion dates. All skills reference it instead of improvising.
- **Shared conventions file** (`references/conventions.md`): current-application resolution (never guess between multiple applications), the two-domain language rule, slug/collision rules, user-owned-file rules.
- **Anti-injection extended plugin-wide:** fetched job postings (apply, Step 1) are now covered by the same source-discipline rule as employer research.
- **Dashboard strategy inverted:** primary output is a self-contained `dashboard.html` (offline, inline CSS); a Live Artifact is an optional extra, honestly labeled (artifacts can't read local files — refresh = regenerate).
- **Writer verifies programmatically:** `wc -w` for the 300–350 word limit, `grep` for banned-word stems, before delivering the letter.
- **build-profile supports incremental updates:** merge new documents into an existing profile, user's manual edits win, ask on conflicts.
- **notes updates the application lifecycle:** logged interactions that imply a status change also update `applicationStatus`.
- apply no longer asks "what do you have?" when the input was already provided.
- Manifest: version bump, keywords. README: removed broken `../PLAN.md` reference.

## 0.1.0

Initial version: 10 skills (apply, init, build-profile, analyze-employer, analyze-role, compare-fit, cover-letter, interview-prep, notes, dashboard) + 2 sub-agents (strategist, writer).
