---
description: A mini-CRM for an application — record free notes and dated contact-log entries (who you spoke with, when, about what, next step). Use when the user wants to log an interaction, jot a thought, or recall their contact history for an application.
---

# Laboramus — Notes (mini-CRM)

Keep lightweight, user-owned notes per application in `notes.md`. Helps the user remember when they last talked to whom and capture thoughts. Written in the **user's language**.

## File: `notes.md` (per application)
Two sections:

```
# Notes — <Display name>

## Thoughts
- (free-form notes the user wants to keep about this application)

## Contact log
| Date | Person (role) | Channel | Summary | Next step |
|------|---------------|---------|---------|-----------|
| 2026-06-24 | Anna Meier (HR) | Call | Discussed timeline; role still open | Send references by Fri |
```

## Behavior
- **Append-only for the log:** never rewrite or delete existing entries. Add new rows.
- **Free notes:** add or edit thoughts as the user wishes.
- Parse natural language: "log that I spoke with Anna from HR today about the timeline, I need to send references by Friday" → a dated contact-log row.
- If `notes.md` doesn't exist, create it with the two sections.
- This file is **purely user data** — no other skill overwrites it. Surface the latest contact date + next step when asked, and the dashboard reads it.

## Date handling
Use today's date for new entries (ask or infer from context if the user references a different day, e.g. "yesterday").
