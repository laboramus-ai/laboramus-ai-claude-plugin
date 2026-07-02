---
description: Sets up the Laboramus workspace folder structure in the current Cowork project. Use when starting with Laboramus for the first time, or when the user asks to set up / initialize their job-application workspace.
---

# Laboramus — Init Workspace

Scaffold the folder structure so the user never has to create folders by hand. Create it inside the current Cowork project folder.

## Create this structure
```
Laboramus/
├── profile/
│   └── source-documents/
│       ├── cv/
│       ├── work-certificates/
│       ├── diplomas/
│       └── personality-tests/        (optional — most users skip)
├── companies/
└── applications/
```

## Steps
1. Create the folders above if they don't already exist. Never overwrite or delete anything that's already there.
2. Briefly explain the layout to the user in their language:
   - `profile/source-documents/` — drop your CV, work certificates, diplomas here. Personality tests are optional.
   - `companies/` — employer analyses, reused across applications at the same company (created automatically).
   - `applications/` — one folder per job application (created automatically).
3. Tell them the natural next step: "Add your CV to `profile/source-documents/cv/` and say 'build my profile' — or paste a job posting and say 'help me apply'."

Keep it short and welcoming. This is a non-technical user's first contact with the tool.
