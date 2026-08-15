# Laboramus AI — Job Application Assistant (Claude Cowork plugin)

Laboramus helps you apply for jobs: it analyzes the **employer** and the **role**, compares them against **your profile**, writes a tailored **cover letter**, prepares you for the **interview**, and keeps a little **CRM** of your contacts — all inside Claude Cowork.

**Version 0.5.3** (early version — see "Status" below).

> 🇨🇭 **Note:** Laboramus AI is currently optimized for the Swiss job market (including integrated door-to-door commute calculations via the Swiss Federal Railways SBB, and local application conventions).

---

## Installation & Updates

Since Laboramus AI is an open-source project, you can easily install it directly from this GitHub repository into your Claude Cowork or Claude Code environment.

### In Claude Cowork (Desktop App)
1. Open the **Settings** (Zahnrad-Symbol) and navigate to **Plugins**.
2. Click on **Hinzufügen** (Add) and select **Marketplace hinzufügen**.
3. Choose **Aus einem Repository hinzufügen**.
4. Enter the following URL into the text field:
   `https://github.com/laboramus-ai/laboramus-ai-claude-plugin`
5. Click **Synchronisieren**.

**Updates:** Claude Cowork will automatically track the "Last updated" date. You can update the plugin through the internal Claude mechanism whenever a new version is released.

### In Claude Code (CLI)
You can install the plugin directly into your global Gemini config directory:
```bash
git clone https://github.com/laboramus-ai/laboramus-ai-claude-plugin.git ~/.gemini/config/plugins/laboramus-ai
```
**Updates:** To update, simply navigate to that folder and run `git pull`.

---

## Use Cases & Skills Overview

Laboramus AI is built around distinct workflows (Use Cases), which are powered by specific underlying tools (Skills). You don't need to call skills manually — you just state your goal, and Claude orchestrates the right skills for the job.

### 1. Profiling: Building your digital twin
Before applying, Claude needs to know who you are.
- **How to use:** Say *"Set up my workspace"*, drop your CV into the created folder, and say *"Build my profile"*.
- **Skills applied:**
  - `init`: Sets up your workspace directory structure.
  - `build-profile`: Analyzes your CV, extracts your hard skills, and structures them into a reusable candidate profile. It also asks for your home address for future commute calculations.

### 2. Job Search: Finding the right positions
Search for matching jobs actively based on your profile's skills without leaving the chat.
- **How to use:** Say *"Search for jobs for me"*.
- **Skills applied:**
  - `search-jobs`: Configures a search profile (e.g., location, title vs. full description) and uses a Chrome-Browser MCP connector to autonomously navigate LinkedIn. It evaluates listings against your profile and logs promising hits into your tracking list.

### 3. Application Orchestration: From Job Ad to Cover Letter
When you find a job you want to apply for, Claude handles the entire deep-dive analysis, fit scoring, and writing process.
- **How to use:** Say *"Help me apply for this job"* and provide the job URL or text.
- **Skills applied (orchestrated by the `apply` skill):**
  - `analyze-employer`: Researches the company's culture and business model. **Bonus:** Automatically calculates the door-to-door commute time (both Public Transit via SBB OpenData and Car via OSRM) from your home address.
  - `analyze-role`: Extracts the true requirements, must-haves, and nice-to-haves from the job posting.
  - `compare-fit`: Matches your profile against the role analysis to highlight strengths, identify gaps, and generate a fit score.
  - `cover-letter`: Drafts a tailored cover letter strategy for your review, and then writes the final, highly authentic letter.

### 4. Interview Preparation
Once invited, you need to prepare for the specific challenges of this role and company.
- **How to use:** Say *"Prepare me for the interview at [Company]"*.
- **Skills applied:**
  - `interview-prep`: Generates a personalized interview strategy based on your previously calculated fit gaps and the employer's culture.

### 5. Application Management & CRM
Keep track of all your ongoing applications and interactions.
- **How to use:** Say *"Show my dashboard"* or *"Log a note that I called the recruiter today"*.
- **Skills applied:**
  - `dashboard`: Generates a self-contained, color-coded HTML dashboard showing all your applications, their status, fit scores, and commute times.
  - `notes`: A mini-CRM that logs your interactions (calls, emails) for specific applications so you always know what the next step is.

---

## Good to know

- **Languages:** your cover letter is always written in the **language of the job posting**. Everything you read (analyses, strategy, dashboard) is in **your** language.
- **Personality tests are optional** — most people skip them. The tool is fully useful without one. When provided, they're used only lightly, never as pseudo-scientific "you fit this role because of your type".
- **Web research** for the employer analysis always **asks first**, tags its sources, and can be turned off. For pages Claude can't read (e.g. LinkedIn), it can use a Chrome-Browser MCP connector / browser tool or guide you to use the *Claude for Chrome* extension.
- **Your notes are yours** — Laboramus only appends to them, never overwrites.

## Status (v0.5)

Early version for testing. The dashboard is a self-contained `dashboard.html` in your `Laboramus/` folder, regenerated on request. Prompts are adapted and condensed from the original Laboramus AI backend. The heavy cover-letter pipeline (originally 5 steps) is condensed into 2: a **strategist** (thinking) and a **writer** (writing).

See `CHANGELOG.md` for what changed between versions.

## Feedback & Support

Found a bug or have a feature request? Since this is an open-source project, all support is handled publicly via GitHub Issues. 
Please create a new issue here: **[Laboramus AI Issues](https://github.com/laboramus-ai/laboramus-ai-claude-plugin/issues)**.

## Privacy & Disclaimer (Datenschutz & Haftungsausschluss)

⚠️ **Important Notice Regarding Your Data & Privacy**

- **Your Data Stays With You:** Laboramus AI operates entirely within your local Claude Cowork environment. As the provider of this plugin, **we have absolutely zero access to your data, your CVs, your application documents, or your Claude.ai account.** All information is stored locally on your machine and processed directly through your personal interaction with Anthropic's Claude. 
- **Personal Responsibility:** Job applications involve highly sensitive personal data. You are solely and completely responsible for how you handle, store, and share this information. By using this plugin, you acknowledge that you process your personal data at your own risk.
- **Swiss Data Protection Act (DSG) & Global Use:** While this plugin is optimized for the Swiss market and aligns with the transparency principles of the revised Swiss Federal Act on Data Protection (FADP / revDSG), the plugin itself does not collect, process centrally, or transmit any data to us. Furthermore, since this tool can technically be downloaded and used globally, we have no control over—and accept no responsibility for—its usage or compliance with other local data protection laws (such as the GDPR).
- **No Liability:** This plugin is provided "as is" without any warranties. The use of this tool is entirely at your own risk. The provider of Laboramus AI explicitly rejects any and all liability for data breaches, data loss, application outcomes, or any direct or indirect damages arising from the use of this plugin.

## For developers

- Plugin manifest: `.claude-plugin/plugin.json`
- Skills: `skills/<name>/SKILL.md`
- Sub-agents: `agents/strategist.md`, `agents/writer.md`
- Shared rules: `references/conventions.md` (cross-skill conventions) and `references/status-schema.md` (the `status.json` contract every skill must follow)
- Local test: `claude --plugin-dir .` (or install the folder in Cowork)

Distribution (git marketplace) is configured in `.claude-plugin/marketplace.json` in this repository.
