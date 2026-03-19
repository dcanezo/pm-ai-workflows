# PM AI Workflows
 
A growing portfolio of AI Agent Skills designed to support and enhance Product Management workflows, thinking, and decision-making.
 
---
 
## Overview
 
This repository contains structured AI Agent Skills built for Product Managers who want to work more intentionally with AI — not just through one-off prompts, but through repeatable, composable systems.
 
Each skill is designed with a clear input, a defined process, and a structured output. They can be used independently or chained together as part of a larger PM workflow — from raw discovery data all the way to execution-ready deliverables.
 
---
 
## Why I Built This
 
Product Management sits at the intersection of customer needs, business goals, and technical feasibility. It involves leading without authority, aligning stakeholders across competing priorities, navigating ambiguity, synthesizing information from multiple sources, and making decisions with incomplete data — all while keeping teams moving forward.
 
AI can significantly augment this work, but only when used with intention and structure. Most PM use of AI today is ad hoc: a prompt here, a summary there. This repository is my attempt to build something more systematic.
 
These skills are designed to:
 
- Reduce decision fatigue by structuring how information is processed
- Accelerate synthesis across research, requests, and feedback
- Surface clear, actionable recommendations — not just summaries
- Create a repeatable workflow that scales as AI tooling matures
 
This is also a living portfolio of how I think about AI-native product work. It will continue to evolve.
 
---
 
## Skill Architecture
 
Skills are organized into three categories, designed to work sequentially:
 
```
AI-Native PM/
├── pm-agent-skills/
│   └── synthesis/              ← Understand the problem
│       ├── research-synthesis/
│       ├── request-synthesis/
│       └── feedback-synthesis/
├── positioning/                ← Define how to position the product
├── prioritization/             ← Decide what to build
│   └── references/
└── creation/                   ← Build the artifacts
    ├── prd-creation/
    │   ├── references/
    │   └── assets/
    ├── epic-creator/
    │   └── references/
    └── pm-ticket-creator/
```
 
### How They Connect
 
**Synthesis** skills take raw inputs — interview notes, feature requests, support feedback — and transform them into structured, evidence-backed insights.
 
**Prioritization** consumes synthesis outputs and produces a decisive, ranked build recommendation with clear reasoning.
 
**Creation** takes prioritized items and generates execution-ready artifacts: PRDs, epics, and user story tickets.
 
Each skill can be used standalone or as part of the full pipeline.
 
---
 
## How to Use
 
Each skill lives in its own folder and contains:
 
- `SKILL.md` — the skill definition, instructions, and output format
- `references/` *(where applicable)* — supporting context, frameworks, or examples the skill draws from
 
### Using with Claude Cowork
 
1. Open Claude Cowork in the Claude Desktop app
2. Point it at this repository folder
3. Tell it which skill to run and provide your input
4. Outputs are saved to the `outputs/` folder
 
### Using with Claude Code
 
1. Navigate to this repository in your terminal
2. Claude Code will automatically read `CLAUDE.md` for project context
3. Provide your input and specify which skill or pipeline to run
4. Outputs are saved to the `outputs/` folder
 
---
 
## About
 
Built by a Product Manager exploring what AI-native product work looks like in practice — not as a novelty, but as a genuine shift in how PMs can operate.
 
This repository is part of a broader mandate to build AI agents capable of supporting the full product development lifecycle.
