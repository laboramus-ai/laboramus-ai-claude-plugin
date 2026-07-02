---
description: Analyzes a job posting to extract the role's requirements — hard/soft skills, responsibilities, seniority, and the soft skills that give an advantage in this kind of role. Use when the user wants to understand what a job requires. Needs NO personal documents.
---

# Laboramus — Analyze Role

Extract what the role *requires*, independent of any candidate. This needs only the job posting — no CV. It lets a user understand a job before uploading anything. Output: `analyses/role-requirements.md`.

(Separate from `compare-fit`, which compares these requirements against the candidate's profile.)

## Input
`job-posting.md` (pasted text or scraped).

## What to extract → `role-requirements.md`
Readable Markdown in the **user's language**:

### Role summary
Title + 2–3 sentences on what the role is about.

### Required hard skills
Each: skill · Must-Have vs. Nice-to-Have (based on posting wording: "required/essential" = Must-Have; "desirable/a plus" = Nice-to-Have) · any specified level/years.

### Required soft skills (explicit + role-typical)
- **Explicit:** soft skills the posting names directly.
- **Role-typical (advantage profile):** the soft skills that *typically give an advantage* in this kind of role, derived from the role itself — even if the posting doesn't spell them out. E.g. a software architect: communication/translation between business and engineering, influence without authority, ambiguity tolerance, long-term/systems thinking, consensus-building. Mark these clearly as "typically advantageous for this role" (a probabilistic guide, not a hard requirement). Keep it grounded and role-specific — not generic platitudes.

### Key responsibilities
The main duties, prioritized (Critical / High / Medium) by prominence in the posting.

### Seniority level of the target role
State the level the role sits at (IC / Lead / Head / C-level). This matters for later fit/career-logic.

### Sparse-posting inference
If the posting is short, infer standard requirements from the job title (e.g. "Business Analyst" → SQL, requirements engineering, stakeholder management) and mark them as inferred, not quoted.

## Next step
If no candidate profile exists yet, tell the user: "This is what the role requires. Upload your CV / build your profile, and I'll compare it against these requirements (the personal fit comparison)."
