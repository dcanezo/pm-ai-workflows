---
name: prioritization
description: "Synthesizes outputs from one, two, or all three PM synthesis skills (research-synthesis, request-synthesis, feedback-synthesis) into a single ranked recommendation that tells a PM what to build next and why. Use this skill whenever you have synthesis outputs to prioritize, need a ranked roadmap view, want to reduce decision fatigue before a planning cycle, or need a stakeholder-ready recommendation. Also triggers when a PM says 'what should we build next', 'help me prioritize', 'rank these findings', 'I need to decide what to focus on', or when a PM has a raw backlog with no synthesis inputs and needs a framework to work through it. Always use this skill when any prioritization decision needs to be made — with or without synthesis inputs."
---

# Prioritization

Transforms synthesis outputs into a decisive, ranked recommendation. This skill sits between Synthesis and Creation — it consumes what the synthesis skills found and tells the PM what to act on first.

It answers three questions:
1. **What should we build next?** — one clear recommendation with reasoning
2. **What are we deferring and why?** — explicit tradeoff framing
3. **How confident are we?** — evidence breadth, data strength, and confidence flags per item

> This skill does not create tickets or execution artifacts. Output is directional, not operational.

---

## Entry Point Detection

Before doing anything else, assess what inputs are available and route accordingly. This is the first step — always.

### Step 0A — Input Quality Check

Scan the provided inputs and classify them:

**Structured synthesis output** — contains recognizable fields from one of the three synthesis skills:
- research-synthesis: Severity, Evidence Strength, Research Status, Insights
- request-synthesis: Demand, Revenue Impact, Discovery Readiness, Affected Clients
- feedback-synthesis: Overall Sentiment, Action, Signals, Sources

**Unstructured / raw input** — does not contain synthesis fields. May be:
- Raw interview notes or research transcripts
- Unprocessed feature requests, emails, or HubSpot exports
- Raw feedback, app store reviews, or support tickets
- A plain backlog list with no scoring or evidence fields
- Mixed or ambiguous content

**If input is unstructured or raw — stop. Do not attempt to score.**

Surface this message to the PM:

> "This input doesn't appear to be a synthesis output. To prioritize reliably, the data needs to be processed through a synthesis skill first. Based on what I can see, here's what I'd recommend:
>
> - Raw interview notes, research, or usability sessions → **research-synthesis**
> - Feature requests, HubSpot exports, or product asks → **request-synthesis**
> - Feedback, app store reviews, NPS, or support tickets → **feedback-synthesis**
>
> If you're unsure which applies, share more context and I'll help you route it. Once synthesis is complete, bring the output back here and we'll prioritize."

If the PM confirms they want to proceed anyway despite the warning — proceed to Path A with all items flagged as `Unstructured input — confidence limited` and apply Tier 2 warnings throughout.

---

### Step 0B — Input Completeness Check

If input passes the quality check, assess completeness:

**Tier 1 — Adapt silently**
One or two fields missing across items. Apply label mapping defaults, flag in output, proceed.
> `Field missing — defaulted to [value]`

**Tier 2 — Adapt and warn**
Multiple critical fields missing on a single item, or critical fields missing on the top-ranked item. Proceed but surface a visible warning.
> `Low confidence — multiple fields missing. Scoring based on defaults. Validate before relying on this ranking.`

**Tier 3 — Stop and challenge**
Triggers when:
- More than 50% of items are missing critical scoring fields
- A synthesis file is provided but contains no structured fields at all
- Input appears to be raw and unprocessed despite being labeled as synthesis output

Surface this message:
> "Too many items are missing critical fields for reliable scoring. Before I proceed, can you confirm these have been processed through a synthesis skill? If the synthesis output is incomplete, I'd recommend re-running the relevant synthesis skill before prioritizing."

---

### Path A — Synthesis-Driven (primary path)
One or more structured synthesis outputs are provided. Proceed to Inputs and Scoring Architecture below.

### Path B — Framework-Driven (fallback path)
No inputs provided at all — PM has nothing yet, not even raw data.

Route to the **Framework Selection Flow** in `references/framework-selection.md`. Ask up to 4 adaptive questions to match the PM to the right prioritization framework for their context.

> Path B is a fallback for when the PM has no data yet — not a workaround for unstructured input. Unstructured input is handled by Step 0A above.

---

## Inputs (Path A only)

### Synthesis Inputs (1–3, any combination)
Accepts outputs from any combination of:
- `research-synthesis` — research themes with Severity, Evidence Strength, Research Status
- `request-synthesis` — feature requests with Demand, Revenue Impact, Discovery Readiness
- `feedback-synthesis` — feedback themes with Sentiment, Action, Signals

**The skill functions with any one input.** When fewer than three are present, the output explicitly states which are missing and notes where confidence may be reduced as a result.

### Runtime Context (all optional)
```
Strategic Orientation: [Risk Mitigation | Growth | Balanced]  (default: Balanced)
Strategic Focus:       [optional string — e.g., "retention", "enterprise expansion"]
CSF Alignment:         [optional string — e.g., "Mobile reliability is critical for enterprise tier"]
OKR Alignment:         [optional string — e.g., "Increase retention rate by 20% by Q4"]
```

None of these are required. The skill produces a valid output without them — but each one sharpens the recommendation. CSFs and OKRs are treated as commitments, not scoring variables — they shape ranking after the base score is computed. Strategic Orientation and Focus are never listed as metadata fields in the output — their influence is translated into plain language within the Executive Summary.

---

## Scoring Architecture (Path A only)

Items are scored through four sequential layers. All components use a standardized 1–5 scale.

### Layer 1 — Base Score

```
Base Score = (Severity × 0.40) + (Impact Breadth × 0.35) + (Evidence Strength × 0.25)
```

#### Severity Scale
| Score | Label | Definition |
|-------|-------|------------|
| 5 | Critical | Blocking, compliance risk, or active churn threat |
| 4 | High | Major workflow impact, no reliable workaround |
| 3 | Medium | Significant friction, workaround exists |
| 2 | Low | Minor inconvenience, low workflow impact |
| 1 | Minimal | Edge case or cosmetic |

#### Impact Breadth Scale
How widely is this problem or request experienced? Mapped per synthesis type:

| Score | Label | Research Themes | Feature Requests | Feedback Themes |
|-------|-------|-----------------|-----------------|-----------------|
| 5 | Very High | 8+ participants, recurring across sessions | 10+ unique accounts | High volume, many distinct submitters |
| 4 | High | 5–7 participants or strong recurrence | 6–9 unique accounts | Moderate-high volume |
| 3 | Medium | 3–4 participants | 3–5 unique accounts | Moderate volume |
| 2 | Low | 2 participants | 1–2 accounts, elevated MRR | Low volume |
| 1 | Isolated | Single mention | 1 account, no deal risk | Single or sparse mentions |

#### Evidence Strength Scale
| Score | Label | Definition |
|-------|-------|------------|
| 5 | Strong | Multi-source, recurring, cross-persona, no contradictions |
| 4 | Moderate-High | Strong signals with minor gaps or one contradiction |
| 3 | Moderate | Some verbatim evidence, partial cross-persona signal |
| 2 | Weak-Low | Single input, mostly paraphrased, or notable contradictions |
| 1 | Weak | Single mention, interpretive only, unvalidated |

#### Synthesis Label Mapping
Map synthesis output labels to numeric scores before scoring:

**From research-synthesis:**
- Severity: High → 4, Medium-High → 4, Medium → 3, Low → 2
- Evidence Strength: Strong → 5, Moderate → 3, Weak → 1
- Research Status: Ready for Design → no penalty, Validate First → flag, Needs Scoping → flag

**From request-synthesis:**
- Demand (as Severity proxy): High → 4, Medium → 3, Low → 2
- Discovery Readiness: Ready → no penalty, Needs More Signal → flag, Deprioritize → flag, Park → exclude
- Revenue Impact: used as override multiplier (see Layer 4)

**From feedback-synthesis:**
- Overall Sentiment (as Severity): Critical → 5, Predominantly Negative → 4, Mixed → 3, Mostly Positive → 2, Predominantly Positive → 1
- Action: Act Now → no penalty, Monitor → note, Amplify → note, Inform → low priority
- Signals: Churn / Compliance → trigger override rules

> See `references/label-mapping-guide.md` for complete mapping tables with worked examples.

---

### Layer 2 — Orientation Adjustment
Applies **selectively to qualifying items only** — not globally to all items.

| Orientation | Adjustment |
|-------------|------------|
| Balanced | 1.0 — no change |
| Risk Mitigation | +15–25% to items carrying churn, trust, or compliance signals |
| Growth | +15–25% to items carrying revenue, adoption, or demand signals |

---

### Layer 3 — Strategic Focus Adjustment
If Strategic Focus is declared, apply +15–25% to items that directly align with the stated focus area.
No adjustment if Strategic Focus is absent.

---

### Layer 4 — CSF / OKR Alignment
These are commitments, not score variables. They shape ranking after the base score is computed.

**CSF (Critical Success Factor) — Constraint Layer**
- Item directly advances a declared CSF → apply multiplier
- Item conflicts with a declared CSF → flag explicitly
- Item is neutral → no adjustment

**OKR — Alignment Layer**
- Item materially moves a declared Key Result → apply alignment boost
- Item does not map to any active OKR → flag as "OKR misaligned this cycle"
- Not every item must tie to an OKR — but the gap must be visible

---

### Override Rules
Applied after all scoring layers, in strict order. These are non-negotiable.

1. **Churn risk** → auto-escalate to top of ranked list regardless of score
2. **Compliance / legal risk** → auto-escalate to top of ranked list regardless of score
3. **Revenue impact** → apply scoring multiplier only. Does not override churn or compliance escalation.
4. **High Severity + Low Evidence** → flag as "Validate before build." Do not auto-escalate. Prevents panic prioritization.

---

## Process (Path A only)

### Step 1 — Ingest & Tag
- Accept all available synthesis outputs as references
- Tag each item by source skill: `[Research]`, `[Request]`, `[Feedback]`
- Note which synthesis skills are present and which are absent
- State confidence impact of any missing inputs upfront

### Step 2 — Map Labels to Scores
- Convert all synthesis labels to 1–5 numeric scale using the mapping tables above
- Flag any items where mapping is ambiguous
- Document the mapped scores — they become the audit trail

### Step 3 — Score Through All Four Layers
- Compute Base Score for each item
- Apply Orientation Adjustment to qualifying items only
- Apply Strategic Focus Adjustment to aligned items
- Apply CSF / OKR multipliers and flags

### Step 4 — Apply Override Rules
- Scan all items for churn, compliance, and revenue signals
- Apply escalation or multiplier in strict order
- Flag High Severity + Low Evidence items for validation

### Step 5 — Rank Within Type
Produce three ranked sub-lists internally before cross-type synthesis:
- Ranked Research Themes
- Ranked Feature Requests
- Ranked Feedback Themes

This prevents raw signal mixing from distorting the unified view. Per-type rankings are internal process steps only — not included in standard output. Available on request.

### Step 6 — Cross-Type Synthesis
Move from per-type rankings to one unified recommendation using this sequence:

**Signal Override**
If any item carries churn or compliance escalation, it surfaces first regardless of type.

**Alignment Check**
If top items across types conflict:
- Surface the tension explicitly in the Executive Summary
- Frame the tradeoff: what each option defends or advances
- Recommend one, explain why the other is deferred
- Use Strategic Orientation or Focus as the tiebreaker if declared

**Confidence Gate**
If the top-ranked item(s) have Evidence Strength ≤ 2 or only one synthesis source contributing → recommend a validation sprint before committing build capacity. Surface with gate applied, do not suppress.

**Tie Handling**
If two items score within 5% of each other → do not force artificial ranking. Surface as a strategic tradeoff and let the PM decide.

### Step 7 — Generate Output

### Step 8 — Post-Output Prompts
Run in this exact sequence. Do not skip or reorder.

**Prompt 1 — Challenge the Priority**
> "This recommendation is based on the available synthesis inputs. Do you have additional context — stakeholder decisions, strategic shifts, account risks, or factors not captured in the references — that should influence this ranking?"

If PM provides context → apply as human override, adjust ranking if warranted, add audit note:
> *"Ranking adjusted based on PM input: [reason]. Original data-driven recommendation was [item]."*

If PM confirms as-is → proceed to Prompt 2.

**Prompt 2 — PRD Handoff**
> "Would you like to start a PRD for [top priority item]?"

If yes → hand off to PRD skill with confirmed top item and supporting context.
If no → proceed to Prompt 3.

**Prompt 3 — Framework Translation**
> "Would you like to translate this recommendation into a stakeholder-friendly framework — such as MoSCoW, RICE, or Value/Effort Matrix?"

If yes → ask which framework, produce a lightweight communication reframe. Underlying recommendation does not change.
If no → close the session.

See `references/framework-selection.md` for framework descriptions and translation guidance.

---

## Output Structure (Path A only)

### Header
```
# Prioritization — [Date]

References:
- [synthesis filename 1]
- [synthesis filename 2]
- [synthesis filename 3]
```

State missing inputs and confidence impact immediately after the header if fewer than three synthesis inputs are present.

---

### Executive Summary

Pure prose. No subheadings except **What We're Deferring**.

1. Lead with the recommendation — what to build and why it wins. One sentence.
2. How it was deduced — synthesis inputs reviewed, posture and focus applied. One to two sentences.
3. Override or gate — state if a churn/compliance override or confidence gate applies. One sentence.

#### What We're Deferring
One brief paragraph — what each deferred item is, why it's deferred this cycle, when to revisit.

---

### Unified Ranking

| Rank | Item | Sources | Final Score | Confidence | Flags |
|------|------|---------|-------------|------------|-------|

**Highlights:**
3–5 bullets. Lead with the most urgent signal. Cover overrides, validation gates, deferrals, misalignment flags.

*Scores calculated using weighted base scoring (Severity 40%, Impact Breadth 35%, Evidence Strength 25%) with strategic focus, orientation, and signal override adjustments applied. Scoring details available on request per item.*

---

### Next Steps

#### Top Recommendation
One to two sentences. Immediate next action, open questions to resolve, handoff details.

#### Deferred Items
One line per item. Specific, testable re-evaluation condition. Ready to be logged to backlog.

> **[Item]** — [condition]. Re-enter prioritization when [threshold or event].

#### Validation Sprints
One block per `Validate before build` item. Grounded in synthesis inputs — not generic advice.

```
[Item] — Validate before build
Signal source: [which input flagged this and why evidence is thin]
Recommended validation: [specific method, participants, what to confirm]
Re-entry condition: [what must be true to re-enter prioritization]
```

---

### Legend

**Confidence**
| Level | Definition |
|-------|------------|
| High | 3 synthesis inputs, Strong evidence, no contradictions |
| Medium | 2 inputs or Moderate evidence, minor gaps |
| Low | 1 input, Weak evidence, or significant contradictions |

**Flags**
| Flag | Definition |
|------|------------|
| Override: Churn | Auto-escalated — active churn signal confirmed |
| Override: Compliance | Auto-escalated — compliance or legal risk confirmed |
| Validate before build | High Severity + Low Evidence — validation sprint recommended |
| Single source | Only one synthesis input contributed — confidence limited |
| Monitor | Negative signal present, no immediate action required |
| OKR misaligned | Item does not map to any active OKR this cycle |
| CSF conflict | Item conflicts with a declared Critical Success Factor |
| Tie | Item scored within 5% of adjacent ranked item — strategic tradeoff surfaced |
| PM Override | Ranking adjusted based on PM-provided context not in synthesis inputs |
| Unstructured input | Item sourced from raw input — confidence limited, synthesis recommended |
| Field missing | Required scoring field absent — default value applied |
| Low confidence | Multiple fields missing — scoring based on defaults, validate before relying on ranking |

---

## Boundary Rules

- **Always run Entry Point Detection first** — quality check before anything else
- **Never score unstructured input** — stop, identify input type, recommend correct synthesis skill
- **Never score when Tier 3 threshold is met** — stop and challenge before proceeding
- **Always adapt silently for Tier 1 gaps** — flag and proceed, do not interrupt the PM
- **Always lead Executive Summary with the recommendation** — what to build, then how it was deduced
- **Executive Summary is pure prose** — no subheadings except What We're Deferring
- **Always make a call** — rank, recommend, explain. Never produce a list without a recommendation
- **Always explain deferrals** — every deferred item needs a reason, not just a lower rank
- **Never force artificial ranking** — use tie handling when items are within 5% of each other
- **Never let revenue override existential risk** — churn and compliance escalate above revenue
- **Never suppress High Severity + Low Evidence items** — surface with validation flag applied
- **Always state missing synthesis inputs** — declare which are absent and note confidence impact
- **Always explain tradeoffs** — frame tension explicitly when top items conflict
- **Never include per-type rankings or scoring details in standard output** — available on request
- **Highlights belong below the Unified Ranking table** — not in the Executive Summary
- **Never list Strategic Orientation or Focus as metadata fields** — translate into plain language
- **Always run Post-Output Prompts in sequence** — Challenge → PRD → Framework Translation
- **Always preserve audit trail on human overrides** — state original recommendation and reason
- **Framework translation is communication only** — never re-scores or changes the recommendation
- **Deferred items must have specific re-evaluation conditions** — "revisit next cycle" is not a condition
- **Validation sprints must be grounded in synthesis inputs** — not generic research advice
- **Never create tickets or execution artifacts** — output is directional, not operational
- **CSFs and OKRs are commitments, not score variables** — apply as multipliers and flags after scoring

---

## Reference Files

- `references/label-mapping-guide.md` — mapping tables from synthesis labels to 1–5 scores, with worked examples
- `references/scoring-worked-examples.md` — end-to-end scoring examples for all four layers
- `references/framework-selection.md` — framework landscape, Path B selection flow, and translation guidance

> Read reference files on demand — only when the relevant path, tier, or prompt is triggered.
