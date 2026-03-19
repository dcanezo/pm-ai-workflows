# Framework Selection Guide

Used in two contexts:
1. **Path B (Fallback)** — No inputs available. Help the PM select and implement a prioritization framework for a raw backlog.
2. **Prompt 3 (Translation)** — Synthesis-driven output already produced. Translate the unified ranking into a stakeholder-friendly framework for communication purposes.

---

## Part 1 — Framework Landscape

### Scoring Frameworks
| Framework | Best For | Requires |
|-----------|---------|---------|
| **RICE** (Reach, Impact, Confidence, Effort) | Data-driven feature ranking | Usage metrics, estimated reach |
| **ICE** (Impact, Confidence, Ease) | Lightweight gut-check scoring | Basic intuition about impact |
| **Value vs. Effort** (2×2 matrix) | Quick wins vs. strategic bets | Rough effort and value estimates |
| **Weighted Scoring** | Custom criteria with stakeholder input | Agreed criteria and weights |

### Strategic Frameworks
| Framework | Best For | Requires |
|-----------|---------|---------|
| **Kano Model** | Classifying features by customer delight | Customer research on satisfaction |
| **Opportunity Scoring** | Rating importance vs. satisfaction gap | Survey data |
| **MoSCoW** (Must/Should/Could/Won't) | Forcing hard choices for a release | Stakeholder alignment session |
| **Buy-a-Feature** | Customer-driven prioritization | Customer participation |

### Contextual Frameworks
| Framework | Best For | Requires |
|-----------|---------|---------|
| **Cost of Delay** | Urgency-based prioritization | Time-sensitivity data |
| **Impact Mapping** | Tying features to business outcomes | Defined goals and metrics |
| **Story Mapping** | User journey-based sequencing | User flow understanding |

---

## Part 2 — Framework Selection Flow (Path B only)

Ask up to 4 adaptive questions. Wait for response before proceeding to the next.

### Question 1 — Product Stage
> "What stage is your product in?"

1. **Pre-product/market fit** — Searching for PMF; experimenting rapidly; unclear what customers want
2. **Early PMF, scaling** — Found initial traction; growing fast; adding features to retain and expand
3. **Mature product, optimization** — Established market; incremental improvements; competing on quality
4. **Multiple products / platform** — Portfolio of products; cross-product dependencies; complex stakeholders

### Question 2 — Team and Stakeholder Environment
> "What's your team and stakeholder environment like?"

1. **Small team, limited resources** — 3–5 engineers, 1 PM, need to focus ruthlessly
2. **Cross-functional team, aligned** — Product, design, engineering aligned; clear goals
3. **Multiple stakeholders, misaligned** — Execs, sales, customers all have opinions
4. **Large org, complex dependencies** — Multiple teams, shared roadmap, cross-team dependencies

### Question 3 — Primary Decision-Making Challenge
> "What's the primary challenge you're trying to solve with prioritization?"

1. **Too many ideas, unclear which to pursue** — Backlog is 100+ items; need to narrow to top 10
2. **Stakeholders disagree on priorities** — Sales wants features, execs want strategic bets
3. **Lack of data-driven decisions** — Prioritizing by gut feel; want a more structured process
4. **Hard tradeoffs between strategic bets vs. quick wins** — Balancing long-term vs. short-term

### Question 4 — Data Availability
> "How much data do you have to inform prioritization?"

1. **Minimal** — New product, no usage metrics, few customers to survey
2. **Some** — Basic analytics, customer feedback, but no rigorous data collection
3. **Rich** — Usage metrics, A/B tests, customer surveys, clear success metrics

### Framework Recommendation Logic

| Stage | Team | Challenge | Data | Recommended Framework |
|-------|------|-----------|------|-----------------------|
| Pre-PMF | Any | Any | Minimal | ICE or Value/Effort Matrix |
| Pre-PMF | Small | Too many ideas | Any | Value/Effort Matrix |
| Early PMF | Aligned | Data-driven | Some | RICE |
| Early PMF | Misaligned | Stakeholder alignment | Any | MoSCoW or Weighted Scoring |
| Mature | Any | Strategic tradeoffs | Rich | Kano or Opportunity Scoring |
| Mature | Any | Urgency | Rich | Cost of Delay |
| Any | Large org | Dependencies | Any | Impact Mapping |

### Framework Output Format (Path B)

```
## Recommended Framework: [Name]

**Why this fits your context:**
- [Rationale tied to Q1–Q4 responses]

**When NOT to use it:**
- [Key limitation]

## How to Implement
### Step 1–4: [Implementation steps]

## Example Scoring Template
[Concrete example with sample table]

## Alternative Framework
If [recommended] doesn't fit, consider [alternative] because [reason].

## Common Pitfalls
1. [Pitfall] — [How to avoid]
```

---

## Part 3 — Framework Translation (Prompt 3 only)

Communication reframe only. Underlying recommendation and ranking do not change.

### MoSCoW Translation

| Unified Ranking Position | MoSCoW Category |
|--------------------------|-----------------|
| Rank 1 — Override: Churn or Compliance | **Must** |
| Rank 1–2 — High confidence, no flags | **Must** |
| Rank 2–3 — Medium confidence | **Should** |
| Rank 4–5 — Low confidence or single source | **Could** |
| Validate before build | **Could** |
| OKR misaligned / Deprioritized | **Won't** |

Output format:
```
## MoSCoW View — [Date]

Must:   [Item] — [one line reason]
Should: [Item] — [one line reason]
Could:  [Item] — [one line reason]
Won't:  [Item] — [one line reason]
```

### RICE Translation

| RICE Component | Maps From |
|---------------|-----------|
| Reach | Impact Breadth score × estimated user base |
| Impact | Severity score (1 = minimal, 3 = massive) |
| Confidence | Evidence Strength as % (Strong=90%, Moderate=60%, Weak=30%) |
| Effort | Not in synthesis — flag as "TBD — requires engineering input" |

Note: RICE scores cannot be fully calculated without Effort. Present Reach × Impact × Confidence and flag Effort as required from engineering.

### Value vs. Effort Matrix Translation

| Quadrant | Criteria |
|----------|---------|
| **Quick Wins** | High final score, no complexity flags |
| **Strategic Bets** | High final score, Needs Scoping flag |
| **Fill-ins** | Low final score, no complexity flags |
| **Time Sinks** | Low final score, Needs Scoping flag |

Note: Effort not captured in synthesis. Flag all placements as "Effort: TBD."

---

## Common Pitfalls (All Frameworks)

1. **Treating scores as gospel** — Frameworks are inputs, not automation. PM judgment overrides when needed.
2. **Framework whiplash** — Stick with one framework for 6–12 months. Switch only when stage/context changes.
3. **Solo PM scoring** — Collaborative sessions (PM + design + engineering) produce more trusted outputs.
4. **Ignoring strategy** — No framework captures strategic importance automatically. Always adjust for vision.
5. **Using RICE without data** — RICE requires Reach estimates. Without usage data, use ICE instead.
