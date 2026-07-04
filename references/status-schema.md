# `status.json` — the one schema every skill uses

Every application folder contains a `status.json`. ALL skills that read or write it MUST use exactly these fields — never invent new field names or shapes.

```json
{
  "displayName": "Acme — Senior Software Architect, Jun 2026",
  "company": "Acme AG",
  "companySlug": "acme-ag",
  "role": "Senior Software Architect",
  "createdAt": "2026-06-24",
  "updatedAt": "2026-07-02",
  "applicationStatus": "preparing",
  "fitScore": 7.5,
  "commute": "35 Min. (1x Umsteigen)",
  "steps": {
    "employer": "2026-06-24",
    "role": "2026-06-24",
    "fit": "2026-06-25",
    "coverLetter": null,
    "interviewPrep": null
  }
}
```

## Field rules
- **displayName** (string) — pretty name shown to the user and on the dashboard.
- **company** (string) · **companySlug** (string, matches `companies/<slug>/`) · **role** (string).
- **createdAt / updatedAt** (ISO date `YYYY-MM-DD`). Set `updatedAt` on EVERY write.
- **applicationStatus** (enum) — the real-world lifecycle of the application:
  `preparing` → `applied` → `interview` → `offer` | `rejected` | `withdrawn`.
  Starts as `preparing`. Update it when the user reports progress ("I sent it", "they invited me", "got a rejection").
- **fitScore** (number 1–10, one decimal) or `null` if compare-fit hasn't run.
- **commute** (string) or `null` — door-to-door commute duration and connection summary (e.g. "35 Min. (1x Umsteigen)"). Calculated in employer step.
- **steps** (object) — one key per pipeline step: `employer`, `role`, `fit`, `coverLetter`, `interviewPrep`. Value = ISO date the step completed, or `null` if not done. No other keys.

## Writing rules
- Read the existing file first; change only the fields you're responsible for; keep everything else as-is.
- If the file is missing or malformed, recreate it with this schema (recover what you can from the folder contents) and tell the user.
