# PM Agent Skills — Workflow Instructions

These instructions define how AI agents should operate within this workspace. Follow them for every task unless a specific SKILL.md overrides a setting.

---

## 1. Workspace Structure

The working directory is `pm-agent-skills/`. It follows this pattern:

- Skills are organized by category. Each category has its own subfolder (e.g., `synthesis/`)
- Each skill lives within its category folder, in its own subfolder named after the skill (e.g., `synthesis/research-synthesis/`)
- Each skill subfolder contains a `SKILL.md` file and may optionally contain a `reference/` folder with supporting documents
- All outputs are saved to the `outputs/` folder at the root of `pm-agent-skills/`

```
pm-agent-skills/
├── INSTRUCTIONS.md
├── outputs/
└── synthesis/
    ├── research-synthesis/
    │   ├── SKILL.md
    │   └── reference/
    ├── request-synthesis/
    │   ├── SKILL.md
    │   └── reference/
    └── feedback-synthesis/
        ├── SKILL.md
        └── reference/
```

---

## 2. Before Running Any Skill

1. Read this `INSTRUCTIONS.md` fully before starting
2. Locate the relevant skill folder and read its `SKILL.md` completely
3. If a `reference/` folder exists within that skill, read all files inside it before proceeding
4. Do not begin execution until all relevant files have been read

---

## 3. Output Behavior

- Save all outputs to the `outputs/` folder at the root of `pm-agent-skills/`
- File format: `.md`
- File naming convention: `YYYY-MM-DD-topic-skill-name.md`
  - `topic` = a short, descriptive label derived from the input content (2–4 words, lowercase, hyphenated)
  - `skill-name` = the name of the skill used (e.g., `research-synthesis`, `feedback-synthesis`)
  - Example: `2026-02-24-missing-logs-research-synthesis.md`
- If a file with the same name already exists, append `-v2`, `-v3`, etc.

---

## 4. Language and Formatting

- Always write in English
- Use Markdown formatting for all outputs
- For output structure and formatting specifics, follow the specifications defined in the skill's `SKILL.md`

---

## 5. When Something Is Unclear

- If anything about the input, the task, or the expected output is unclear, **pause and ask before proceeding**
- Do not make assumptions and proceed silently — surface ambiguity early

---

*This file is a living document. Update it as your workflow evolves.*
