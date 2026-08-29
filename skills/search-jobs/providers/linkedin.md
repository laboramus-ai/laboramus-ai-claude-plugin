# Provider: LinkedIn

## Platform Information
- **Name:** LinkedIn
- **Key:** `linkedin`
- **Supported Work Models:** On-site, Remote, Hybrid

## Search URL Formulation Rules

When forming a search URL for LinkedIn, use the following base pattern:
`https://www.linkedin.com/jobs/search/?keywords=<encoded_keywords>&location=<encoded_location>&f_WT=<work_model_codes>`

**Work Model Codes (`f_WT` parameter):**
- `1` = On-site
- `2` = Remote
- `3` = Hybrid
- Combine them with commas if multiple are selected (e.g., `f_WT=1,3` for On-site + Hybrid).

**Date / Recency Filters:**
- `f_TPR=r86400` = Past 24 hours
- `f_TPR=r604800` = Past week
- `f_TPR=r2592000` = Past month
- `sortBy=DD` = Sort by most recent (always combine with a date filter for freshness scans)

**Distance:**
- `distance=<km>` = Search radius in km from the location centre (e.g., `distance=40`)

**Company Filter:**
- `f_C=<companyId>` = Restrict results to a specific company (use the LinkedIn numeric company ID)

**Search Depth Nuances:**
- **Title-Only match (narrow):** Wrap the primary job title in double quotes in the `keywords` parameter.
- **Broad match:** Pass keywords without quotes.

## Extraction Instructions
- Wait for the job list on the left side to fully render before extracting.
- Scroll down the list pane to load more jobs if necessary (LinkedIn lazy-loads results).
- If direct job URLs are not visible in the DOM, use a JavaScript snippet to extract all `a[href*="/jobs/view/"]` links from the page before navigating away.
- Extract per job: Job Title, Company, Location, direct Job URL (not the search URL), date posted / recency label, applicant count if shown, and a brief snippet.

## Authentication Note
LinkedIn requires a logged-in session to see full job details and applicant counts. Always access LinkedIn via the user's Chrome browser (Mac Mini + Claude-in-Chrome connector) — never via cloud WebFetch, which will hit a login wall or receive degraded content.
