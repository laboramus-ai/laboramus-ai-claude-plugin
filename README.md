# Laboramus AI — Job Application Assistant (Claude Cowork plugin)

Laboramus helps you apply for jobs: it analyzes the **employer** and the **role**, compares them against **your profile**, writes a tailored **cover letter**, prepares you for the **interview**, and keeps a little **CRM** of your contacts — all inside Claude Cowork.

**Version 0.5.2** (early version — see "Status" below).

---

## What it does

| Skill | What it does |
|-------|--------------|
| **apply** | The main entry point — just say "help me apply for this job". It figures out the rest. |
| **init** | Sets up your workspace folders (once). |
| **build-profile** | Turns your CV / certificates / diplomas into a reusable profile. |
| **analyze-employer** | Researches the company: culture, values, pros & cons. |
| **analyze-role** | Extracts what the job requires (works even without your CV). |
| **compare-fit** | Compares the role's requirements against your profile: matches, gaps, fit score. |
| **cover-letter** | Writes a tailored cover letter — first a strategy you can review, then the letter. |
| **interview-prep** | A personalized interview prep pack. |
| **notes** | A mini-CRM: log who you talked to and when. |
| **dashboard** | An overview of all your applications in one place. |
| **search-jobs** | Searches for matching jobs on LinkedIn using candidate profile & Chrome browser. |

## How to use it (non-technical)

1. **Install** the plugin (your administrator/distributor will tell you how — typically `/plugin install laboramus-ai` from a marketplace).
2. In Claude Cowork, create or open a **Project** folder for your job search.
3. Say **"set up Laboramus"** → it creates the folders.
4. Put your **CV** (and any work certificates / diplomas) into `Laboramus/profile/source-documents/`, then say **"build my profile"**.
5. For each job: say **"help me apply"** and either paste the job posting text or give the URL.
6. Review the **strategy** it shows you, tweak anything, then ask it to **write the cover letter**.
7. Ask for **interview prep**, **log contacts** as you talk to people, and open the **dashboard** anytime for an overview.

You never have to create folders or files by hand — just talk to Claude.

## Good to know

- **Languages:** your cover letter is always written in the **language of the job posting**. Everything you read (analyses, strategy, dashboard) is in **your** language.
- **Personality tests are optional** — most people skip them. The tool is fully useful without one. When provided, they're used only lightly, never as pseudo-scientific "you fit this role because of your type".
- **Web research** for the employer analysis always **asks first**, tags its sources, and can be turned off. For pages Claude can't read (e.g. LinkedIn), it can use a Chrome-Browser MCP connector / browser tool or guide you to use the *Claude for Chrome* extension.
- **Your notes are yours** — Laboramus only appends to them, never overwrites.

## Status (v0.5)

Early version for testing. The dashboard is a self-contained `dashboard.html` in your `Laboramus/` folder, regenerated on request. Prompts are adapted and condensed from the original Laboramus AI backend. The heavy cover-letter pipeline (originally 5 steps) is condensed into 2: a **strategist** (thinking) and a **writer** (writing).

See `CHANGELOG.md` for what changed between versions.

## For developers

- Plugin manifest: `.claude-plugin/plugin.json`
- Skills: `skills/<name>/SKILL.md`
- Sub-agents: `agents/strategist.md`, `agents/writer.md`
- Shared rules: `references/conventions.md` (cross-skill conventions) and `references/status-schema.md` (the `status.json` contract every skill must follow)
- Local test: `claude --plugin-dir .` (or install the folder in Cowork)

Distribution (git marketplace) is configured in `.claude-plugin/marketplace.json` in this repository.
