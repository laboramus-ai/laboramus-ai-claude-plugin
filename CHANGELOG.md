# Changelog

## 0.5.2 — 2026-07-04

Integrated door-to-door SBB commute time calculation (OpenData.ch).

- **SBB Commute Calculation**: Integrated automatic door-to-door commute time check during `analyze-employer` step using the Swiss transport OpenData REST API.
- **Home Address Setting**: Added prompting flow to ask and store the user's home address under `### Preferences` in their candidate profile when first run.
- **Dashboard Columns**: Added commute duration display column to the main applications table.
- **Strict Schema Update**: Expanded `status.json` contract to officially document the `"commute"` field.

## 0.5.1 — 2026-07-04

Refined `/search-jobs` preferences, skill matching, and portal options.

- **Search Preferences**: Added portal selector configurations, search filters for what/where parameters.
- **Skill Verification**: Enabled explicit user verification of extracted skills before search queries are executed.
- **Search Depth Control**: Added Title-Only (narrow) and Full Description (broad) matching depth options.

## 0.5.0 — 2026-07-04

Added `/search-jobs` skill to automate and monitor job searches on LinkedIn.

- **Job Search Skill**: Created new skill `skills/search-jobs/SKILL.md` to analyze candidates' profile, define named search profiles, construct LinkedIn job search queries, and run them via Chrome browser MCP connector.
- **Job Leads Tracker**: Defined a JSON tracking database (`search-profiles.json` and `job-search-tracker.json`) to persist preferences and monitor search status.
- **Workflow Linkage**: Integrated job leads with application pipeline initialization.

## 0.4.1 — 2026-07-03

Added integration with Chrome-Browser MCP connector for failing URLs.

- **Browser Connector Integration**: Updated `apply` and `analyze-employer` skills to offer and use the Chrome-Browser MCP connector (`browser_subagent`) to fetch LinkedIn and other JS-heavy/blocked job postings.
- **Documentation**: Updated README to reflect version `0.4.1`.

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
