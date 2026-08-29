# Provider: jobs.ch

## Platform Information
- **Name:** jobs.ch
- **Key:** `jobs.ch`
- **Language:** German-first (Swiss job market)
- **Supported Work Models:** all (filter available on-site; limited URL-level control)

## Search URL Formulation Rules

Use the following base pattern:
`https://www.jobs.ch/de/stellenangebote/?term=<encoded_query>&location=<encoded_location>&radius=<km>&sort=date`

**Key parameters:**
- `term` = search query, URL-encoded (e.g., `Head+of+Engineering`, `Leiter+Informatik`)
- `location` = city name, URL-encoded (e.g., `Z%C3%BCrich` for Zürich)
- `radius` = radius in km around the location (e.g., `40`)
- `sort=date` = most recent first (always include for freshness scans)

**Important:** Do NOT use the `location` + `region` + `query` parameter format — it drops the query on redirect. Always use `term=` as the query parameter.

**Example URL:**
`https://www.jobs.ch/de/stellenangebote/?term=Head+of+Engineering&location=Z%C3%BCrich&radius=40&sort=date`

## Detail Page
Each job listing has a detail URL in the format:
`https://www.jobs.ch/de/stellenangebote/detail/<UUID>/`

If detail URLs are not visible directly in the DOM (jobs.ch lazy-loads them), use a JavaScript snippet to extract all `a[href*="/de/stellenangebote/detail/"]` links from the page before navigating away.

## Effective German Search Keywords (Engineering Leadership)
Use multiple separate searches to cover the Swiss German market:
- `Head of Engineering`
- `Leiter Informatik`
- `Leiter Softwareentwicklung`
- `Chef Informatik`
- `Bereichsleiter Informatik`
- `Head of Technology`
- `VP Engineering`
- `CTO`

## Work Model
jobs.ch does not expose work model as a clean URL parameter. Work model (Home Office, Hybrid, Vor Ort) appears as a badge on the listing card and in the job description. Extract it from the listing text.

## Extraction Instructions
- jobs.ch renders job listings as cards in a scrollable list.
- Scroll to load all results if the count exceeds one page.
- Extract per job: Job Title, Company (if shown — may be anonymised), Location, Detail URL, date posted, and salary range if visible.
- If the employer is listed as anonymous (e.g., "Rocken®" as recruiter, employer hidden), note this explicitly in `notes`.
- Navigate to the detail page for full job description before scoring.

## Authentication Note
jobs.ch is accessible via WebFetch for public listings. However, for full page rendering and lazy-loaded content, prefer the Chrome browser connector (Mac Mini). If WebFetch returns incomplete results or misses job cards, switch to Chrome automatically.
