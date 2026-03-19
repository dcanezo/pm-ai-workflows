# PRD Section Guide

Detailed instructions and examples for each PRD section.

---

## Executive Summary

**Purpose:** Give skimmers (leadership, stakeholders) everything they need in one paragraph.

**Format:** Two paragraphs.
- First paragraph: context and problem — what exists today and what's missing
- Second paragraph: what this PRD covers and what the goal is

**Tone:** Confident and clear. No hedging. This is your pitch.

**Tip:** Write it first to force clarity. Refine it last once all sections are complete.

---

## Problem Statement

**Purpose:** Make the problem feel real, urgent, and undeniable.

**Structure:**
- **What is the problem?** — Describe the situation and friction clearly. Lead with this to establish context before narrowing to who.
- **Who has this problem?** — Be specific. Name the persona, not just "users."
- **Why is it painful?** — User impact AND business impact.
- **Evidence** — Quotes, data, support tickets, interviews. This is what separates a real PRD from a hypothesis.
- **Consequences of not solving** — What happens if we do nothing?

**Tone:** This section should make the reader feel the pain. Use specific numbers, real quotes, and concrete consequences.

**Anti-pattern:** "Users want better onboarding." ← No evidence, no specificity, no urgency.

---

## Target Users & Personas

**Purpose:** Define who you're building for so everyone makes decisions with the same person in mind.

**Structure:**
- **Primary Persona** — Name, role, company context, goals, pain points, current behavior
- **Secondary Persona(s)** — If relevant
- **Jobs-to-be-done** — "When I [situation], I want to [motivation], so I can [outcome]."

**Tip:** Keep personas grounded in research. Avoid fictional archetypes that don't reflect real discovery.

---

## Strategic Context

**Purpose:** Answer "why this, why now" for anyone who might question prioritization.

**Always include — scale the depth:**

**Minimum for any feature (even small ones):**
One sentence answering: *"Why are we doing this now and not in 6 months?"*
This is a forcing function. Without it, deferred scope items have no principled reason for being deferred.

**Full section for large initiatives:**
- Business Goals / OKR / CSF Alignment
- Market context and "why now" trigger
- Competitive landscape
- Defensible moat (only if genuine and relevant)

**Tone:** Strategic, not academic. This should feel like a business case, not a market research report.

---

## Solution Overview

**Purpose:** Describe what you're building at the right level of abstraction — enough for alignment, not so detailed it removes design's agency.

**Structure:**
- Opening paragraph describing the solution in plain language (no "High-Level Description" subheading needed)
- **Key Capabilities** — What does it do? Not how it looks — that's Design's job.
- **Before / After table** — Powerful for stakeholder alignment; shows pain point → solution at a glance

**Anti-pattern:** Specifying UI details, pixel dimensions, or exact copy. Keep it principle-level.

---

## Phased Scope

**Purpose:** Show the full end-to-end vision while making clear what's being built now vs. later. Replaces the flat "Out of Scope" section.

**When to use full phasing:** Any feature with multiple logical delivery increments, technical prerequisites, or a v2+ vision.

**When to keep it simple:** Truly standalone features with no planned follow-on work — a simple In Scope / Out of Scope is fine.

**Format:**
```markdown
### v1 — [Descriptive label]
**In scope:**
- [What's being built]

**Out of scope for this version:**
- [What's deferred and why — one line rationale for each]

### v2 — [Descriptive label]
**In scope:**
- [What's being built next]

### v3+ — Future Consideration
- [Longer-term vision items]
```

**Tip:** Version labels should be descriptive, not just numbers. "v1 — Foundation & Core Detection" tells a story. "v1" doesn't.

**Tip:** Every deferred item needs a one-line rationale. "Not in v1" is not a reason. "Validate core experience first before adding complexity" is.

---

## Success Metrics

**Purpose:** Define what "done well" looks like so the team can validate whether the feature succeeded.

**Structure:**
- **Primary metric** — The one number you're optimizing for
- **Secondary metrics** — Supporting indicators
- **Targets** — Current state → Goal (e.g., "Activation rate: 40% → 60%")
- **Notes** — How will you measure this? What's the baseline?

**Tip:** If you can't define a success metric, the problem statement probably isn't clear enough yet.

| Metric | Definition | Target | Notes |
|--------|-----------|--------|-------|
| Primary metric | What you're measuring | Current → Goal | How to track |
| Secondary metric | Supporting signal | Current → Goal | How to track |

---

## User Stories & Requirements

**Purpose:** Give cross-functional teams a human-level picture of what's being built. Illustrative, not ticket-ready.

**Structure:**
- **Epic Hypothesis** — The strategic bet: "We believe that [solution] will [outcome] for [persona]. We'll know this is true when [metric]."
- **User Stories** — Format: "As a [persona], I want to [action], so that [outcome]."
- **Acceptance Criteria** — Maximum 3–4 per story. If you need more, you're too deep — that's the Epic Builder's job.
- **Edge Cases & Constraints** — Number these. What happens in unusual scenarios? What are the known technical boundaries?

**Critical rule:** PRD user stories convey intent and scope. They are inputs to the Epic Builder skill, not specs for direct development. Keep acceptance criteria at the intent level, not the implementation level.

**User Story Format:**
```
**Story N: [Short title]**
As a [persona], I want to [action], so that [outcome].

Acceptance Criteria:
- [ ] [Intent-level criterion — what should be true, not how]
- [ ] [Intent-level criterion]
- [ ] [Intent-level criterion — max 4 total]
```

---

## Dependencies & Risks

**Purpose:** Surface blockers and assumptions early so the team can plan around them.

**Structure:**
- **Dependencies** — Technical, team, and external dependencies with owners where known
- **Risks & Mitigations** — What could go wrong and how you'd address it

**Format:**
```
Risk: [Description]
Mitigation: [How we'll address it]
```

---

## Open Questions

**Purpose:** Document genuinely unresolved decisions so they don't get lost or assumed away.

**Only include here:**
- Things the user genuinely doesn't know yet
- Decisions requiring input from another team or stakeholder
- Design or product decisions not yet made

**Do NOT include here:** Anything answered during the PRD conversation — incorporate those answers directly into the relevant section.

**Format:**
```
- [Question]? → Status: [Unresolved / Owner: Name / Decision: X]
```

**Tip:** Open Questions is a sign of intellectual honesty, not incompleteness. The goal is to make real unknowns visible so they get resolved before engineering starts.
