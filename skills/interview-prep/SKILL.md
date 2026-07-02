---
description: Creates a personalized interview preparation pack — likely questions with model-answer outlines, smart questions to ask the employer, and prep tips. Use after an application has a strategy brief / analyses. Output is readable Markdown.
---

# Laboramus — Interview Prep

A leaf step: it consumes existing artifacts and produces `interview-prep.md`. Nothing depends on it. Written in the **user's language**.

## Inputs (use what exists)
`strategy-brief.md`, `analyses/employer.md`, `analyses/fit-comparison.md`, `analyses/role-requirements.md`, `job-posting.md`, `profile/candidate-profile.md`.

## Output → `interview-prep.md`

### 1. Interview questions (15–20, in 4 categories)
- **Standard HR** (3–4): personalized versions of classics (strengths, weaknesses, goals) — based on the candidate's *real* profile, never generic.
- **Skill gaps** (2–4): questions targeting the gaps from fit-comparison and their mitigations. Only if real gaps exist.
- **Behavioral / STAR** (3–4): "Tell me about a time when…" tied to concrete experiences in the profile and requirements in the role.
- **Motivation** (2–3): "Why this company? / Why this role?" grounded in the employer analysis and the candidate's actual career logic.

(No cultural-fit category — we don't run cultural-fit analysis.)

For each question give:
- the question,
- **why it's asked** + which analysis it derives from,
- **difficulty** (easy / medium / hard),
- a **model-answer outline** (3–5 bullet points — NOT a full scripted answer),
- the **strength to highlight** (from profile/brief),
- a **pitfall to avoid**.

### 2. Questions to ask the employer (5–7)
Smart questions across culture / role / growth / team / practical. For ones answerable from the employer analysis, give a suggested answer; for ones needing insider knowledge, note that.

### 3. Prep tips (3–5)
Specific to THIS application, not generic advice.

## Rules
Personalization is mandatory — no generic questions without context. Everything traces to the analyses. Outlines, not scripted answers. If a personality summary exists, use it only as reinforcement (the "does it help?" rule).
