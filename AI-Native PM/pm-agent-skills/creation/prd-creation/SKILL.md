---
name: prd-creation
description: >-
  Creates a complete Product Requirements Document (PRD) that blends strategic storytelling with engineering-ready structure. Use this skill whenever a user wants to write, draft, or create a PRD, product spec, or requirements document — whether they're starting from a rough idea, a brief, or structured outputs from synthesis and prioritization skills. Also trigger when a user says things like "I want to document this feature", "help me write up this initiative", "I need a spec for engineering", or "turn this into a PRD". Assesses input quality section by section before drafting — asks only for what's genuinely missing. Supports both one-shot and interactive modes.
---

# PRD Creation Skill

## Purpose

Transform product ideas, discovery findings, or synthesis outputs into a complete, stakeholder-ready PRD — one that tells a compelling story for leadership *and* gives engineering the clarity they need to build.

A great PRD answers two questions simultaneously:
- **"Why does this matter?"** — for leadership, stakeholders, and cross-functional teams
- **"What exactly are we building?"** — for engineering, design, and QA

---

## Defensive Input Principle

This skill never assumes it's receiving perfect input. Whether the input comes from a PM's synthesis outputs, a prioritization skill, or a rough verbal brief — always assess what's available before drafting.

**The goal is surgical, not binary.** Don't evaluate input as simply "rich" or "thin." Instead, map what's available to each PRD section and identify exactly where the gaps are. You may have enough to draft sections 1–4 confidently but need to ask targeted questions before drafting sections 5–8. Ask only for what's genuinely missing — never ask for something you can reasonably infer from context.

---

## Step 1: Assess Input & Choose Mode

Before writing anything, evaluate available information section by section:

| PRD Section | What you need to draft it confidently |
|-------------|--------------------------------------|
| Executive Summary | Problem + solution + impact (draft last) |
| Problem Statement | Who, what, why, at least one evidence signal |
| Target Users & Personas | Persona name, role, pain point, behavior |
| Strategic Context | At minimum: one sentence on why now and not later |
| Solution Overview | High-level description of what's being built |
| Phased Scope | Whether delivery is phased; what's in v1 vs. later |
| Success Metrics | At least one primary metric with a directional target |
| User Stories | Core user actions and expected outcomes |
| Dependencies & Risks | Known blockers or assumptions |
| Open Questions | Unresolved decisions needing other stakeholders |

**If you have enough for all sections** → go directly to **One-Shot Mode**.

**If you have gaps in specific sections** → go to **Interactive Mode**, asking only about the missing sections.

**If the user explicitly requests a mode** → respect their choice. Honor "just draft it" or "walk me through it."

---

## Step 2: Interactive Mode — Clarifying Questions

Ask questions in logical groups. Never ask about something you can infer. Never ask all questions at once if the input is mostly complete — be surgical.

**Tier 1 — Always ask if missing:**
1. What is the feature or initiative name?
2. What problem does it solve, and who experiences it?
3. Who are the primary users?
4. Will this be delivered in phases (v1, v2, etc.) or all at once? If phases, what's the minimum you need to ship first to deliver real value?
5. What does success look like? Even a rough idea helps.

**Tier 2 — Ask if initiative seems large, strategic, or phased:**
6. Is this tied to a specific business goal, OKR, or CSF?
7. Is there a "why now" trigger — competitive pressure, spike in churn, regulatory change, or a strategic window?
8. Are there known technical dependencies or constraints?

**Tier 3 — Ask only if genuinely unclear:**
9. What's explicitly out of scope for the first version?
10. Are there open questions that require input from other teams or stakeholders?

> **Rule:** If you can reasonably infer an answer, make the call and note your assumption. Only surface it as an Open Question if it requires another stakeholder to resolve or if it's a significant assumption that could change scope.

**Handling Open Questions:**
Only include something in the Open Questions section of the final PRD if:
- The user genuinely doesn't know yet ("I'll check with Engineering")
- It requires input from another team or stakeholder to resolve
- It's a design or product decision that hasn't been made yet

Do NOT put something in Open Questions if the user answered it during the conversation — incorporate the answer directly into the relevant PRD section.

---

## Step 3: Draft the PRD

Use the structure below. Depth scales with initiative size:
- **Small feature / epic** → concise, focused; Strategic Context is one sentence minimum
- **Large initiative / new product** → full storytelling, rich strategic context, detailed metrics

### Tone & Style Guide

- Write like a PM who is also a storyteller. Blend narrative prose with structured lists — avoid bullet-only sections in Problem Statement and Executive Summary.
- Executive Summary and Problem Statement should pull the reader in, not just list facts.
- Strategic Context should answer "why this, why now" in a way that a skeptic would find compelling.
- User Stories and Dependencies must be precise — engineering will use these to scope work.

### User Stories Discipline

PRD user stories are **illustrative, not ticket-ready**. Their job is to convey intent and scope so cross-functional teams understand what's being built. They are inputs to the Epic Builder skill — not specs for direct development.

**Enforce this rule:** No more than 3–4 acceptance criteria per PRD user story. If you find yourself writing more, you are going too deep. Pull back to intent. The Epic Builder will handle decomposition.

---

## PRD Structure

```
# [Feature/Product Name] PRD

## Executive Summary
## Problem Statement
## Target Users & Personas
## Strategic Context
## Solution Overview
## Phased Scope
## Success Metrics
## User Stories & Requirements
## Dependencies & Risks
## Open Questions
```

See `references/section-guide.md` for detailed instructions and examples for each section.

---

## Strategic Context — Always Include, Scale the Depth

Strategic Context is **never optional** — but the depth scales with initiative size.

**Minimum for any feature (even small ones):**
> One sentence answering: *"Why are we doing this now and not in 6 months?"*

This is a forcing function. Without it, deferred scope has no principled reason for being deferred — it's just deferred.

**Full section for large initiatives:**
- Business Goals / OKR / CSF Alignment
- Market context and "why now" trigger
- Competitive landscape
- Defensible moat (only if genuine and relevant)

---

## Phased Scope Section

This replaces the flat "Out of Scope" section. For any feature with phased delivery, structure scope explicitly by version.

**Format:**

```markdown
## Phased Scope

### v1 — [Descriptive label, e.g. "Foundation & Core Detection"]
**In scope:**
- [What's being built]

**Out of scope for this version:**
- [What's deferred and why]

### v2 — [Descriptive label]
**In scope:**
- [What's being built]

### v3+ — Future Consideration
- [Longer-term vision items]
```

**Versioning questions to ask during clarification:**
- Is this being built in phases or all at once?
- What's the minimum shippable version that delivers real value to users?
- What's the logical sequence — what needs to exist before the next thing can be built?
- Are there technical prerequisites (API, infrastructure) that form their own phase?

If the PM hasn't thought through phasing yet, help them. Probe with: "What would you ship first if you had to deliver something in 4 weeks?" — this usually surfaces the natural v1 boundary.

---

## Step 4: Present & Refine

After drafting, present the full PRD and note:
1. Any assumptions made that should be validated
2. Any sections that could be strengthened with more information
3. Explicitly flag: *"The user stories in this PRD are illustrative — they're intended as inputs for the Epic Builder skill, not for direct ticket creation."*

Then iterate based on feedback.

---

## Skill Chain Context

This skill sits at the start of the creation chain:

**PRD (this skill) → Epic Builder → pm-ticket-creator**

- PRD user stories are **illustrative** — they convey intent and scope, not implementation detail
- The **Epic Builder** takes PRD output and produces properly structured epics with INVEST-compliant user stories
- **pm-ticket-creator** takes Epic Builder output and produces individual, development-ready tickets

Each skill in this chain is **standalone by default, composable by design** — it works independently with any input, but produces better output when fed from the previous skill.

---

## Output Format

Deliver the PRD as a well-formatted Markdown document. Save to `/mnt/user-data/outputs/[feature-name]-PRD.md`.

The final document should feel like something a PM would be proud to share in a leadership review — not a template with blanks filled in, but a document that reflects genuine thinking about the product.

---

## Reference Files

- `references/section-guide.md` — Detailed instructions and examples for each PRD section
- `references/anti-patterns.md` — Common PRD mistakes and how to avoid them
- `assets/template.md` — Blank PRD template for reference
