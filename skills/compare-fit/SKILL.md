---
description: Compares the candidate's profile against a role's requirements — matches, gaps, fit score, strengths, development areas, and a recommendation. Use after the role requirements and the candidate profile both exist. Needs the personal profile.
---

# Laboramus — Compare Fit

Put "what the role needs" next to "what I bring" and produce an honest fit assessment. Requires both a candidate profile and the role requirements. Output: `analyses/fit-comparison.md`.

## Inputs
- `analyses/role-requirements.md` (from analyze-role; if missing, run that first — don't recompute requirements here).
- `profile/candidate-profile.md` (the candidate). If absent, stop and tell the user to build their profile first.
- `analyses/employer.md` if present (context).

## What to produce → `fit-comparison.md`
Readable Markdown in the **user's language**, addressing the user directly ("you"):

### Fit score (1–10) + explanation
Honest and realistic. Explain the reasoning.

### Hard skills
Required vs. yours → matches (you meet/exceed) and gaps (missing/insufficient). Quote the requirement and cite your evidence (level, years, context from the profile).

### Soft skills
Same structure. If a personality summary exists in the profile, use it ONLY as reinforcement for soft-skill claims already evidenced by certificates — never as the sole basis (the "does it help?" rule). If no personality data, ignore it.

### Career logic — seniority check (critical)
Compare your highest prior role to the target role's seniority:
- **Step up** (e.g. Senior → Lead): logical progression.
- **Lateral** (Senior → Senior): logical continuation.
- **Step down / overqualified** (e.g. Head-of → IC): do NOT call it "a logical next step". Name it a strategic pivot/step down. **Apply a scoring penalty: the fit score MUST NOT exceed 7.5**, and state "risk of overqualification / flight risk" explicitly in the explanation.

### Anti-inflation (sparse postings)
If the posting was thin, score against the *inferred* standard requirements too. Don't award 8–10 just because the candidate matches the few explicit words — if standard implied skills are missing, cap lower (max 6–7).

### Strengths (for THIS role)
Top 3–5, specific to this role, not generic.

### Development areas
2–3 concrete, addressable gaps.

### Recommendation
Should you apply? What to emphasize, what to prepare for. Actionable.

## Honesty
A poor fit is valuable information — don't sugarcoat. Evidence-based throughout; cite the profile. No invented skills (if a skill isn't in the profile, it's a gap, not an assumption).

After finishing, update the application's `status.json` with the fit score.
