---
name: research-synthesis
description: "Synthesizes qualitative research inputs (interview notes, surveys, usability tests, diary studies, field observations) into structured, evidence-traceable, decision-ready artifacts for product managers. Use this skill whenever the user wants to analyze or synthesize research notes, interview notes, user feedback, or any qualitative PM input — even if they just say 'help me make sense of these notes' or 'what are the patterns here?' Handles single or multiple inputs, adapts to research phase (Discovery, Validation, Usability, Evaluative), and produces structured theme-level synthesis with atomic insights, opportunity statements, and HMW questions."
---

# Research Synthesis

Transforms qualitative research inputs into structured, defensible synthesis artifacts. Unlike Feedback Synthesis (which processes sentiment at scale) and Request Synthesis (which aggregates feature demand), this skill answers three questions:

1. **What are users struggling with?** — pain points and their functional and emotional impact
2. **How confident are we in each finding?** — evidence strength, stability, and coverage gaps
3. **What should we explore next?** — opportunity statements, HMW questions, and research gaps

---

## Methodological Foundations

- **Affinity Mapping & Thematic Clustering** — cluster by topic first, tag persona inside clusters
- **Evidence Traceability** — every insight cites its source; all inferences are flagged as assumptions
- **Opportunity Framing** — problem-grounded opportunity statements in Discovery mode only
- **Jobs-to-be-Done** — Pain / Impact / Workaround as the default atomic insight structure
- **Signal Weighting** — frequency × intensity × diversity × phase-fit × contradiction penalty

---

## Input Types

Research Synthesis explicitly supports multiple input types. Each carries different evidence weight:

| Input Type | Evidence Weight | Notes |
|------------|----------------|-------|
| Interview notes | Deep, small sample | Verbatim quotes carry full weight; paraphrased notes carry moderate weight |
| Surveys | Broader patterns, self-reported | Higher stability when n is large; lower directness than interviews |
| Usability sessions | Behavioral friction in controlled context | Observed behavior outweighs self-reported; controlled context limits generalizability |
| Diary studies | Longitudinal, in-the-moment behavior | High contextual richness; captures what users do, not just what they say |
| Field observations | Contextual realities users may not articulate | Highest directness; small sample typical |

**Key distinction:** Weight findings differently based on what users *say* vs. what they *do* vs. what is *directly observed*. A recurring friction observed across 50 survey responses or multiple usability sessions has higher stability than a theme from 5 interviews. Field observations and diary studies surface behaviors users may not be able to articulate in interviews.

**Evidence directness:**
- Verbatim quote → full weight
- Paraphrased summary → moderate weight; flag if PM-authored
- Interpretive statement → lower weight; flag with ⚠️ Assumption

---

## Input Handling

Accept inputs in any of these forms:

1. **MCP-connected documents** — files via Notion, Google Drive, Jira, or connected tools
2. **Pasted notes** — raw text pasted directly into the prompt
3. **Uploaded files** — .md, .txt, .pdf, or .docx

**Before synthesizing, detect:**
- Input type — interview, survey, usability, diary study, field observation, or mixed
- Number of sources
- Evidence directness distribution
- Research phase — ask if not stated: Discovery / Validation / Usability / Evaluative
- Product context (recent releases, known issues) — optional but helps explain patterns

**Guard against double amplification:** inputs are often already partially synthesized by the PM. When input is interpretation-heavy, flag it and weight evidence accordingly.

---

## Research Phases

| Phase | Purpose | Opportunity Statement? |
|-------|---------|----------------------|
| Discovery | Exploring unknown problems, no solution yet | Yes |
| Validation | Testing whether a proposed solution solves the right problem | No |
| Usability | Testing whether users can use a built solution | No |
| Evaluative | Assessing a shipped feature against intended outcomes | No |

---

## Process

### Step 1 — Parse, Tag & Classify
- Separate verbatim quotes from paraphrased notes from interpretive statements
- Tag each unit with: persona (if identifiable), topic area, input type
- Flag temporal signals: "used to," "before the update," "since we switched"
- Flag leading questions or interviewer-introduced bias with ⚠️ Bias signal

### Step 2 — Cluster into Themes
- Group by topic first, then tag persona inside each cluster
- Two items belong to the same theme if they share 2+ of: same product area, same emotional response, same root cause
- Where the same pain appears across multiple personas, mark explicitly — this is a high-signal finding
- Apply thin data thresholds: 3+ items → theme; 2 items → Early Signal flagged explicitly; 1 item → Single Mention, document for traceability only

### Step 3 — Build Atomic Insights
For each discrete insight within a theme, populate the simplified JTBD structure:
- **Pain** — what the user experiences
- **Impact** — functional and emotional consequences in one paragraph
- **Workaround** — what they do instead, if anything
- **Evidence** — verbatim quote or paraphrase with source ID and directness label
- **Stability** — Early Signal / Emerging Pattern / Strong Pattern

Flag any inferences with ⚠️ Assumption.

### Step 4 — Score Evidence Strength
Express as Strong / Moderate / Weak with a one-sentence explanation. Internal factors:
- Frequency — how many participants or responses mentioned it
- Intensity — language strength
- Diversity — does it appear across personas or only one segment?
- Phase fit — is this the right signal type for the stated phase?
- Contradiction — does conflicting evidence exist? Apply a penalty.

### Step 5 — Assign Research Status
- **Ready for Design** — evidence is strong enough to move to design if prioritized
- **Validate First** — promising signal but evidence is too thin to act on
- **Needs Scoping** — finding is clear but has unresolved technical or feasibility questions

### Step 6 — Flag Signals
Actively scan for: Churn / Compliance / Trust / Shadow System

### Step 7 — Handle Contradictions
- Present splits explicitly — "3 of 5 users report X; 2 of 5 report the opposite"
- Offer a reconciliation hypothesis if supportable, labeled as ⚠️ Assumption
- Never silently resolve contradictions — unresolved tension is itself a signal

### Step 8 — Write Opportunity Statements (Discovery mode only)
Each theme gets one Opportunity Statement + one How Might We question.

**Opportunity Statement format:**
A pure problem statement — who is affected, what is broken, and what it costs them. No solution language.

> "Field workers in low-signal areas cannot reliably confirm their attendance was recorded, causing incorrect absence records and pay loss with no available workaround."

**How Might We format:**
Reframes the problem as an open design question. A good HMW question is grounded in a real synthesized insight, focused on the underlying user need (not a proposed feature), specific enough to define a clear user and moment, yet open enough to allow multiple solution directions. It should avoid naming solutions and avoid vague ambition. Instead, it reframes the tension in a way that guides exploration without constraining it.

Good: "How might we help field workers trust that their attendance was captured, even when working in environments where GPS or connectivity is unreliable?"
Too narrow: "How might we add an offline mode to the clock-in screen?"
Too broad: "How might we improve mobile reliability?"

The Opportunity Statement anchors the finding. The HMW opens the design space without closing it.

### Step 9 — Identify Research Gaps
For each unresolved contradiction, weak-evidence insight, or ⚠️ Assumption, generate a specific follow-up question. Format: "Validate whether [assumption] by [method] with [target]."

---

## Output Structure

### Header
```
# Research Synthesis — [Topic] — [Phase] — [Date]

Time Window: [start] to [end]

Total [Interviews / Surveys / Sessions] Reviewed: [N]
```

### Executive Summary
A brief overview paragraph followed by 3–5 highlight bullets. Lead with the most severe finding.

### Coverage Gaps
Bullet list of what the research did not capture — personas not represented, segments underrepresented, known issues still open during research. Always placed before the overview table so the reader interprets findings with appropriate context.

### Research Overview Table
```
| # | Theme | Severity | Participants | Research Status | Signals |
|---|-------|----------|-------------|-----------------|---------|
```

### Research Themes
Each theme as a numbered section using this structure:

---

## [N]. [Theme Name]

[1–2 sentence neutral description of what the research surfaced.]

### Severity: [Label]
Labeled **[Label]** — [one sentence explaining why, focused on impact, not restating the description above.]

### Evidence Strength: [Label]
[One sentence — what drives the rating: sample size, verbatim evidence, cross-persona signal, contradictions.]

### Research Status: [Label]
[One sentence explaining what this means for next steps.]

### Insights

**[Insight ID] — [Short title]**

- **Pain**: [What the user experiences]
- **Impact**: [Functional and emotional consequences in one paragraph]
- **Workaround**: [What they do instead, or None]
- **Evidence**: "[Quote or paraphrase]" — [Source ID] (verbatim / paraphrased)
- **Stability**: [Early Signal / Emerging Pattern / Strong Pattern] — [brief note]

⚠️ Assumption: [Any inference made — stated explicitly]

### Signals
- [Signal type] — [brief explanation]

### Opportunity Statement *(Discovery mode only)*

[Pure problem statement — who, what is broken, what it costs them. No solution language.]

*How might we [reframe the problem as an open design question, specific to user and moment, open to multiple solutions]?*

---

### Contradictions & Unresolved Signals
Each contradiction stated explicitly with split evidence and reconciliation hypothesis labeled as ⚠️ Assumption.

### Research Gaps & Next Steps
One validation question per gap, assumption, or unresolved signal. Format: "Validate whether [assumption] by [method] with [target]."

### Traceability Map
Lightweight table mapping each Insight ID to its source(s).

```
| Insight ID | Description | Source |
|------------|-------------|--------|
```

### Legend
Always include at the bottom as tables covering: Severity, Evidence Strength, Research Status, Insight Stability, Signals.

**Severity**
| Severity | Definition |
|----------|------------|
| High | Directly impacts pay, compliance, or core workflow with no available workaround |
| Medium–High | Wrong outcomes with high downstream impact; workaround exists but is unreliable |
| Medium | Friction or wrong outcomes but correctable; workaround exists |
| Low | Minor inconvenience; low workflow impact |

**Evidence Strength**
| Evidence Strength | Definition |
|------------------|------------|
| Strong | Multiple participants, verbatim evidence, cross-persona signal, no contradictions |
| Moderate | Some verbatim evidence, partial cross-persona signal, or small sample |
| Weak | Single participant, paraphrased only, or significant contradictions present |

**Research Status**
| Research Status | Definition |
|----------------|------------|
| Ready for Design | Evidence is strong enough to move to design if prioritized |
| Validate First | Promising signal but evidence is too thin to act on |
| Needs Scoping | Finding is clear but has unresolved technical or feasibility questions |

**Insight Stability**
| Stability | Definition |
|-----------|------------|
| Strong Pattern | 4+ mentions or high participant diversity |
| Emerging Pattern | 2–3 mentions or cross-persona signal |
| Early Signal | 1 mention, unvalidated, needs further research |

**Signals**
| Signal | Definition |
|--------|------------|
| Churn | Participant explicitly considering alternatives or recommending competitor |
| Compliance | Regulatory or legal exposure implied by the finding |
| Trust | Finding reflects damaged confidence in the product's reliability or accuracy |
| Shadow System | Users maintaining tools outside the product to compensate for a gap |

---

## Boundary Rules

- **Never propose solutions** — Opportunity Statements describe problems only; HMW questions open the design space without prescribing solutions
- **Opportunity Statements and HMW questions in Discovery mode only**
- **All inferences labeled** as ⚠️ Assumption — never presented as fact
- **Contradictions never silently resolved** — always surfaced explicitly
- **Never state persona when not identifiable** from the source — describe role implied by context only, or omit
- **Never force themes from thin data** — apply the clustering thresholds in Step 2
- **Coverage Gaps always before the overview table** — the reader must know the blind spots before reading the findings

---

## Reference Files

- `references/output-examples.md` — annotated example outputs
- `references/evidence-strength-guide.md` — scoring rubric with worked examples per input type

> Read these on demand when you need worked examples or scoring guidance.
