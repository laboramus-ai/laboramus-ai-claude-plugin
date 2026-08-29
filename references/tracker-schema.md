# `job-search-tracker.json` — schema reference

The file `profile/job-search-tracker.json` is the central tracking database for all job search activity. Every skill and scheduled task that touches search results, leads, or company monitoring MUST read this schema and write only valid fields.

---

## Top-level structure

```json
{
  "lastSearchDate": "YYYY-MM-DD",
  "searchProfiles": ["<profile name>"],
  "focusedCompanies": [...],
  "leads": [...],
  "watchedCompanies": [...],
  "searchesRun": [...],
  "searchesRun_localRadar": [...],
  "nextActions": [...]
}
```

---

## `focusedCompanies` — high-priority company watch list

Companies the candidate would apply to immediately if a suitable role opens. Checked daily by automated tasks.

```json
{
  "company": "Acme AG",
  "location": "Zürich (On-site)",
  "ovMinutes": 30,
  "careersUrl": "https://acme.com/careers",
  "linkedInUrl": "https://www.linkedin.com/company/acme/jobs/",
  "focusReason": "Why this company is in focus",
  "scanFrequency": "daily-weekdays",
  "alertThresholdFitScore": 65,
  "linkedInAlertActive": false,
  "checkedAt": "YYYY-MM-DD",
  "currentOpenRoles": ["Role A", "Role B"],
  "notes": "Free text"
}
```

**Field rules:**
- `ovMinutes` — door-to-door public transit time in minutes from the candidate's home address.
- `scanFrequency` — one of `daily-weekdays`, `weekly`, `manual`.
- `alertThresholdFitScore` — minimum fitScore to trigger a push alert and add to `leads`.
- `linkedInAlertActive` — true if a LinkedIn Job Alert is set up for this company.
- `currentOpenRoles` — list all currently visible open positions (any level), not just matching ones. Updated on every check.

---

## `leads` — evaluated job postings

```json
{
  "jobId": "acme-head-eng-2026",
  "title": "Head of Engineering",
  "company": "Acme AG",
  "location": "Zürich (Hybrid)",
  "url": "https://www.linkedin.com/jobs/view/12345/",
  "portal": "linkedin",
  "postedDate": "YYYY-MM-DD",
  "fitScore": 78,
  "status": "lead",
  "workModel": "Hybrid",
  "pensum": "100%",
  "notes": "Free text evaluation",
  "foundAt": "YYYY-MM-DD"
}
```

**`status` lifecycle:** `lead` → `applying` → `applied` → `interview` → `offer` | `rejected` | `withdrawn` | `dismissed`

**`portal` values:** `linkedin`, `jobs.ch`, `indeed`, `direct`, `xing`, `other`

**`fitScore`** — integer 0–100. Use these bands as a guide:
- 80–100: Excellent match, apply immediately
- 65–79: Good match, evaluate and apply
- 50–64: Partial match, flag for review
- below 50: Poor match, dismiss unless special reason

---

## `watchedCompanies` — passive radar

Companies observed but not yet in active focus. Checked weekly or manually.

```json
{
  "company": "Acme AG",
  "location": "Zürich (ÖV ~30 Min ab Fehraltorf)",
  "reason": "Why this company is on radar",
  "linkedInSlug": "acme-ag",
  "linkedInAlert": false,
  "checkedAt": "YYYY-MM-DD",
  "notes": "What was found on last check",
  "linkedInUrl": "https://www.linkedin.com/company/acme-ag/jobs/"
}
```

---

## `searchesRun` — portal search log

One entry per portal search query executed. Never delete entries — append only.

```json
{
  "portal": "jobs.ch",
  "query": "Leiter Informatik",
  "location": "Zürich",
  "radius": "40km",
  "filter": "sort=date",
  "date": "YYYY-MM-DD",
  "resultCount": 76,
  "newLeadsFound": 1,
  "notes": "Optional context"
}
```

---

## `searchesRun_localRadar` — geographic area / company radar log

One entry per local radar sweep (geographic area or company cluster check).

```json
{
  "type": "Firmen-Radar <Area>",
  "date": "YYYY-MM-DD",
  "area": "Optional area description",
  "companiesChecked": ["Company A – result", "Company B – result"],
  "newLeadsFound": 0,
  "leadsFound": ["Optional list of found leads"],
  "conclusion": "Summary of what this radar found"
}
```

---

## `nextActions` — prioritised action list

Plain string array, ordered by priority. Prefix urgent items with `🚨`. Prefix focus-company alerts with `🚨 FOKUS-FIRMA:`. Updated by every skill and scheduled task that creates new work.

---

## Writing rules

1. Read the existing file before writing — never overwrite the whole file, merge your changes.
2. Append to arrays (`leads`, `searchesRun`, etc.) — never remove existing entries.
3. Update `lastSearchDate` to today whenever a portal search runs.
4. `nextActions` is a managed list — remove completed items and add new ones; do not let it grow unboundedly.
5. If the file is missing or malformed, recreate the top-level structure with empty arrays and tell the user.
