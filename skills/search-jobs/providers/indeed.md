# Provider: Indeed

## Platform Information
- **Name:** Indeed
- **Key:** `indeed`
- **Supported Work Models:** Remote (reliable), On-site / Hybrid (use location string instead)

## Search URL Formulation Rules

When forming a search URL for Indeed, use the country-appropriate domain and the following base pattern:
`https://www.indeed.<tld>/jobs?q=<encoded_keywords>&l=<encoded_location>&sort=date`

Use `.ch` for Switzerland, `.de` for Germany, `.com` as fallback.

**Work Model Codes (`sc` parameter):**
- Remote: append `&sc=0kf%3Aattr(DSQF7)%3B`
- On-site / Hybrid: omit `sc` and rely on the location string — Indeed does not have reliable URL-level filters for these modes.

**Recency:**
- `&fromage=<days>` = Jobs posted in the last N days (e.g., `&fromage=7` for past week, `&fromage=1` for today)

**Search Depth Nuances:**
- **Title-Only match (narrow):** Prefix the query with `title:` (e.g., `q=title:(Head of Engineering)`).
- **Broad match:** Pass keywords normally without prefix.

## Extraction Instructions
- Extract: Job Title, Company, Location, direct Job URL, salary range (if visible).
- **CAPTCHA:** Indeed may show a CAPTCHA. If detected, pause and instruct the user to solve it manually in the browser, then resume.

## Authentication Note
Indeed Switzerland (`indeed.ch`) may be accessible via WebFetch for public listings, but always prefer the Chrome browser connector for complete results and to avoid bot-detection blocks.
