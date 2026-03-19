---
name: epic-creator
description: Generate well-scoped Epics for product initiatives, each representing a meaningful chunk of user value with a clear Definition of Done and a list of child User Story titles. Use when a PM has a PRD, feature brief, or initiative idea and needs to structure the work into Epics before writing individual tickets. Triggers on phrases like "create an epic", "break this into epics", "structure this initiative", "what epics do I need for this", or when a PRD has been completed and the next step is execution planning.
---

# Epic Creator

## Purpose
Generate one or more well-scoped Epics for a product initiative. Each Epic represents a meaningful chunk of user value — not just a technical container — and serves as the organizing structure for individual User Story tickets in Jira or Notion.

**Where this fits in the workflow:**
`PRD → Epic Creator (this skill) → pm-ticket-creator (individual User Story tickets)`

---

## Step 1: Gather Context

Before generating Epics, ensure you have enough information. If a PRD is provided, extract what you can from it and only ask for what's missing.

**If no PRD is provided, ask for the following:**

1. **What is the feature or initiative?** (Brief description of what's being built)
2. **Who are the users affected?** (Personas or roles)
3. **What problem does this solve?** (The core user or business pain)
4. **What module or product area does this touch?** (Free-form — e.g., "Resolution Center on Mobile", "Leave Module", "ReadyCash")
5. **How large is this initiative?** (Rough sense — small tweak, medium feature, large multi-sprint effort)
6. **Are there any known constraints or dependencies?** (Technical, timeline, compliance, etc.)

**If a PRD is provided:**
- Extract all of the above from the PRD
- Only ask clarifying questions for information that is genuinely missing or ambiguous
- Never ask for information already present in the PRD

---

## Step 2: Assess Epic Count

Before generating, determine how many Epics this initiative warrants. Use the splitting guidance in `references/splitting-patterns.md` to inform this judgment.

**Single Epic is appropriate when:**
- The initiative is small and delivers one clear user outcome
- Work can be completed in 1-2 sprints
- There is no natural boundary between phases or user groups

**Multiple Epics are appropriate when:**
- The initiative spans multiple sprints with distinct deliverable phases
- Different user groups experience different value (e.g., employee vs. manager)
- There are independent workstreams that could ship separately
- The scope is large enough that one Epic would contain 8+ User Stories

**Always advise the user:**
- State your recommendation (single or multiple) and briefly explain why
- If multiple, explain the proposed boundaries between Epics
- Ask for confirmation before proceeding: *"I'd recommend splitting this into [N] Epics because [reason]. Does that make sense, or would you like to adjust?"*

---

## Step 3: Generate the Epics

For each Epic, produce the following structure:

---

### Epic Title
`[Module / Product Area] | [Specific Feature]`

*Examples:*
- `Resolution Center on Mobile | Missing Logs API`
- `Leave Module | Multi-Level Approval Flow`
- `ReadyCash | Loan Eligibility Engine`

Keep titles concise and scannable. The module/area and specific feature should be clear enough that someone reading a Jira backlog immediately knows what this Epic is about.

---

### Problem
What user or business problem does this Epic solve? Write 2-4 sentences.
- Ground this in the user's experience, not technical requirements
- Be specific about who is affected and what breaks down today without this

---

### Solution / Expected Results
What will be built, and what does it enable? Write 2-4 sentences or use brief bullets for complex deliverables.
- Focus on outcomes and capabilities, not implementation details
- Avoid prescribing exact technical solutions

---

### Definition of Done
*"This Epic is complete when [user can do X / system can do Y]."*

One to two sentences maximum. This is the PM's north star for the Epic — when this condition is met, the Epic closes.

**Quality checks:**
- ✅ Describes an observable user or system outcome
- ✅ Specific enough to be verifiable
- ❌ Not "when all stories are closed" (that's a process condition, not a value condition)
- ❌ Not vague like "when the feature is live"

---

### User Stories (Titles Only)
A list of task-style story titles that belong to this Epic. These become the direct inputs to `pm-ticket-creator` when writing individual tickets.

Format: Simple numbered list, task-style (not "As a [persona]..." format)

*Example:*
1. Display missing logs in Resolution Center timeline
2. Fetch missing log data via API integration
3. Handle empty state when no logs are available
4. Add missing log filter to Resolution Center search

**Guidelines:**
- Each title should be specific enough to become a standalone ticket
- Aim for 3-7 stories per Epic; if you're exceeding 8, consider splitting the Epic further
- Titles should reflect user-facing behavior, not pure technical tasks ("Add API endpoint" is too technical; "Fetch missing log data via API integration" is better)

---

## Step 4: Validation Nudge (For Net-New or Uncertain Features)

If the initiative is **net-new** (a new module, a new product, or a feature with no existing user demand signal), add a brief advisory after the Epics:

> ⚠️ **Validation Note:** This initiative appears to be net-new. Before committing full engineering effort, consider a lightweight validation — a prototype test, a feature interest survey, or a concierge trial with a pilot client. Epics with validated demand reduce the risk of building the wrong thing.

**Do NOT include this note for:**
- BAU improvements to existing features
- Compliance or regulatory work
- Contractually committed client requirements
- Bug fixes or technical debt

Use judgment. If it's clearly committed work, skip the note entirely.

---

## Step 5: Present and Iterate

- Present all Epics in the format above
- Ask: *"Does this structure make sense? Would you like to adjust the Epic boundaries, titles, or story list?"*
- Allow iteration on any section
- If the user wants to proceed to ticket writing, remind them: *"You can now use pm-ticket-creator for each User Story title above."*

---

## Output Format

```
## Epic 1: [Module | Specific Feature]

**Problem**
[2-4 sentences]

**Solution / Expected Results**
[2-4 sentences or bullets]

**Definition of Done**
This Epic is complete when [observable outcome].

**User Stories**
1. [Story title]
2. [Story title]
3. [Story title]
...

---

## Epic 2: [Module | Specific Feature]
[Repeat structure]
```

---

## References

- `references/splitting-patterns.md` — Read this when assessing how many Epics to generate and where to draw the boundaries. Contains the 9 Humanizing Work splitting patterns for scoping decisions.
