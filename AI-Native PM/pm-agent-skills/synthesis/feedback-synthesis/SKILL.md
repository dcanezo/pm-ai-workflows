---
name: feedback-synthesis
description: "Synthesizes raw feedback from multiple sources (app store reviews, in-app forms, NPS/CSAT responses, support tickets, CS/AM notes, social media) into structured sentiment intelligence with problem signals and routing recommendations. Use this skill whenever you have a batch of feedback to process and need to understand: how users feel (sentiment), what's driving those feelings (problem signals), and where patterns exist across sources and personas. Distinct from Request Synthesis — this skill handles how users feel and what's broken, not explicit feature asks. Automatically flags embedded feature requests for routing to Request Synthesis."
---

# Feedback Synthesis

Transforms raw feedback from any source into structured sentiment intelligence. Unlike Research Synthesis (which models user problems in depth) and Request Synthesis (which aggregates feature demand), this skill answers three questions:

1. **How do users feel?** — sentiment scored at theme, source, and persona level
2. **What's driving those feelings?** — problem signals extracted from negative and mixed sentiment
3. **What needs to go elsewhere?** — embedded feature requests flagged and routed to Request Synthesis

---

## Methodological Foundations

- **Multi-level sentiment analysis** — sentiment measured at three levels: overall theme, per source (app store vs. NPS vs. support, etc.), and per persona. Each level reveals different things.
- **Sentiment as signal, not score** — a number means nothing without the pattern behind it. Every sentiment score is paired with the evidence that drove it.
- **Problem-first extraction** — negative and mixed sentiment is always unpacked into the underlying problem, not left as a vague complaint.
- **Request detection & routing** — feedback that contains an explicit feature ask is flagged and routed to Request Synthesis rather than synthesized here. Keeps both skills clean.
- **Source credibility weighting** — not all feedback sources carry equal weight. A support ticket represents a user actively blocked; an app store review may be emotional and unverified. Source context is preserved in every signal.

---

## Input Handling

Accept inputs in any of these forms:

1. **MCP-connected repository** (primary): Query the feedback repository, HubSpot, Zendesk, or connected tools directly
2. **Uploaded files or pasted content** (secondary): CSV exports, Notion docs, .md or .txt files
3. **Mixed sources** (common): Combine multiple — deduplicate and tag each item by source

**Tag every feedback item with its source before processing:**
- App store review
- In-app feedback form
- NPS/CSAT response
- Support ticket
- CS/AM note
- Social media / community post

**Also accept as optional context:**
- Persona definitions — for persona-level sentiment breakdown
- Previous synthesis outputs — for trend comparison
- Product context (recent releases, known issues) — helps explain sentiment spikes

---

## When to Use This Skill

**Use when:**
- You have a batch of feedback to process (any volume)
- You need to understand sentiment patterns before a roadmap review
- Stakeholders are citing individual complaints and you need the full picture
- Post-launch feedback review after a release
- Regular cadence review (weekly/bi-weekly)

**Don't use when:**
- Feedback is already synthesized into problem signals
- You only have 1–3 items (read them directly)
- All items are explicit feature requests with no sentiment context (use Request Synthesis)

---

## Process

### Step 1 — Ingest, Tag & Deduplicate

- Tag each item by source (see icons above)
- Normalize to one feedback item per entry
- Remove exact duplicates; preserve source references
- Note total items received, sources represented, and date range in output header

### Step 2 — Detect & Route Embedded Feature Requests

Before sentiment analysis, scan each item for explicit feature asks:

**A feedback item contains an embedded request if it includes:**
- "I wish it had..."
- "Can you add..."
- "It would be better if..."
- "Missing feature: ..."
- Any explicit ask for new functionality

**When detected:**
- Extract the request statement
- Flag it with 🔀 Route to Request Synthesis
- Note the source item it came from
- Continue processing the remaining sentiment content if any

Do not synthesize the request portion here. Keep it clean.

### Step 3 — Assign Sentiment per Item

Score each feedback item:

| Sentiment | Signal |
|-----------|--------|
| 😊 Positive | Satisfaction, delight, praise, recommendation |
| 😐 Neutral | Factual, no strong emotion, mixed positive/negative |
| 😞 Negative | Frustration, complaint, disappointment, churn language |
| 🚨 Critical | Severe negative — churn signal, trust breach, compliance concern |

### Step 4 — Cluster into Feedback Themes

Group feedback items by shared subject matter using the same clustering logic as Research Synthesis:

**Two items belong to the same theme if they share 2+ of:**
- Same product area or workflow
- Same emotional response (frustration, confusion, delight)
- Same root cause or trigger

**Cluster by:** what users are reacting to, not how they phrased it
**Not by:** source, persona, or sentiment polarity (a theme can contain both positive and negative feedback)

### Step 5 — Score Sentiment at Two Levels

For each theme, calculate sentiment at two levels:

**Level 1 — Theme Sentiment**
Overall sentiment for this theme across all feedback. Express as a label: Critical / Predominantly Negative / Mixed / Mostly Positive / Predominantly Positive.

**Level 2 — Sentiment by Role (where identifiable)**
Break down sentiment within the theme by role or persona — but only where the source explicitly identifies or clearly implies the role. See Persona Attribution rules. Omit this level entirely if no roles are identifiable from the sources in this theme.

### Step 6 — Extract Problem Signals from Negative Sentiment

For every theme with Predominantly Negative or Critical sentiment, the opening description should surface the underlying problem neutrally. The Overall Sentiment explanation then explains why it earned that label. The Action explanation then explains what to do and why now.

### Step 7 — Assign Action

For each theme, assign one of:
- **Act Now** — compliance deadline, active churn risk, or critical regression actively blocking users
- **Monitor** — negative signal but no immediate deadline; watch for escalation in next batch
- **Amplify** — strong positive sentiment with advocacy or upsell potential
- **Inform** — neutral or positive baseline; worth documenting but no action needed this cycle

### Step 8 — Flag Signals

Actively scan for:
- **Churn** — language like "cancelling," "switching," "looking for alternatives," or CS-flagged renewal risk
- **Compliance** — regulatory or legal language, audit references
- **Trust** — data concerns, reliability complaints, broken promises
- **Delight** — strong positive sentiment worth amplifying
- **Viral** — social media posts with high engagement potential

### Step 9 — Identify Trends

If a previous feedback synthesis is provided as context:
- Note sentiment direction per theme: Improving / Worsening / Stable
- Flag new themes that didn't appear previously
- Flag themes where volume has spiked

If this is the first run: state "Baseline — no prior batch to compare against" for every theme's Trend field.

---

## Feedback Theme Template

Use the Output Structure section above as the definitive format. Key field rules:

- **Overall Sentiment**: Explain why it earned the label — focus on what drove the sentiment, not what the problem is (the opening description covers that)
- **Action**: Explain why this specific action is recommended right now — what makes it urgent, worth watching, worth amplifying, or simply informational. Always a separate explanation from Overall Sentiment.
- **Evidence**: 2–3 representative quotes or paraphrases. Only include quotes from sources where content is explicitly available — do not fabricate or infer quotes.
- **Sentiment Breakdown**: Persona attribution rules — see Persona Attribution section below
- **Signals**: Use sub-bullets. Churn / Compliance / Trust / Viral / Delight only.
- **Trend**: If prior synthesis available, state direction. If first run, state "Baseline — no prior batch to compare against."
- **Sources**: Each entry includes source type, IDs where available, sentiment, and brief description of content.

## Output Structure

### Header
```
# Feedback Synthesis — [Date]

Time Window: [start] to [end]

Total Feedback Items Reviewed: [N]
```

### Executive Summary
A brief overview paragraph of the feedback batch, followed by 3–5 highlight bullets. Themes should be ordered: Critical and Act Now first, then Predominantly Negative, then Positive.

### Feedback Theme Overview Table
```
| # | Theme | Overall Sentiment | Action | Signals |
|---|-------|------------------|--------|---------|
```
One row per theme, ordered by severity (Critical first) then Action (Act Now before Monitor).

### Feedback Themes
Each theme as a numbered section using this structure:

---

## [N]. [Theme Name]

[1–2 sentence neutral description of what users are reacting to.]

### Overall Sentiment: [Label]
Labeled **[Label]** — [one sentence explaining why it earned this sentiment label, not restating the opening description.]

### Action: [Label]
[One sentence explaining why this specific action is recommended — what makes it urgent, worth watching, worth amplifying, or simply informational.]

### Evidence
- "[Quote or paraphrase]" — [Source type, Role if explicitly identified]
- "[Quote or paraphrase]" — [Source type, Role if explicitly identified]

### Sentiment Breakdown
- [Role or source-implied context]: [Sentiment] — [brief note]
- [Role or source-implied context] (inferred from context): [Sentiment] — [brief note]
- Omit entirely if persona is not identifiable from any source in this theme

### Signals
- [Signal type] — [brief explanation with supporting context]

### Trend
[If prior synthesis available: Improving / Worsening / Stable / New theme — one sentence.]
[If first run: Baseline — no prior batch to compare against.]

### Sources
- [Source type] — [N] [sentiment] ([IDs if available]) — [brief description of what was said]

---

### Routed to Request Synthesis
A table of all embedded feature requests detected. Documented for traceability — do not synthesize as feedback signals.

```
| Feature Request | Source | Persona | Request Synthesis Reference |
|----------------|--------|---------|----------------------------|
```

### Legend
Always include at the bottom of every output as tables:

**Overall Sentiment**
| Sentiment | Definition |
|-----------|------------|
| Critical | Majority of feedback indicates blocking, compliance, or churn-risk issues |
| Predominantly Negative | Most feedback expresses frustration, friction, or distrust |
| Mixed | Feedback is split between positive and negative signals |
| Mostly Positive | Most feedback is satisfied with minor concerns noted |
| Predominantly Positive | Strong positive sentiment with few or no negative signals |

**Action**
| Action | Definition |
|--------|------------|
| Act Now | Immediate response needed — compliance deadline, active churn risk, or critical bug |
| Monitor | Negative signal but no immediate deadline — watch for escalation |
| Amplify | Positive signal worth engaging — testimonials, CS follow-up, social response |
| Inform | Neutral baseline — worth documenting but no action needed this cycle |

**Signals**
| Signal | Definition |
|--------|------------|
| Churn | Account explicitly considering alternatives or flagged for renewal risk |
| Compliance | Legal or regulatory exposure |
| Trust | Data, privacy, or reliability concern eroding confidence in the product |
| Viral | Public amplification — positive or negative — that may affect brand perception |
| Delight | Strong positive signal worth amplifying for advocacy, testimonials, or upsell |

---

## Thin Data Handling

Not all batches will have 30+ items. Apply these thresholds:

| Volume | Handling |
|--------|----------|
| 3+ items pointing to the same pattern | Surface as a theme |
| 2 items | Surface as an Early Signal — flag explicitly as "Early Signal — needs more data before acting" |
| 1 item | Do not surface as a theme — document in a brief "Single Mentions" section at the bottom for traceability |

**Never force themes from sparse data.** If a batch only supports 2 themes, produce 2 themes. Do not pad with weak signals to fill a template.

---

## Persona Attribution

Feedback sources vary widely in how much identity information they carry. Apply these rules strictly:

| Evidence | Rule |
|----------|------|
| Source explicitly identifies role, job title, or account type | State it directly — "HR Admin," "Operations Manager," "SunGroup HRIS Lead" |
| Context clearly implies a role (e.g., ticket about approving requests → manager role) | State it with "(inferred from context)" |
| Anonymous source — app store review, unknown in-app submission, social post | Omit persona attribution entirely. Do not guess. |

**Never name product-specific personas** (e.g., "Employee," "Manager" as defined by a specific product). Describe the role implied by the feedback context only. This keeps the skill portable across any product.

---

## Boundary Rules

- **Never synthesize embedded feature requests** — flag and route to Request Synthesis only
- **Never report sentiment without evidence** — every theme needs representative quotes
- **Never collapse source-level differences** — app store negativity is not the same as CS note negativity; preserve source context in the Sources section
- **Never force sentiment resolution** — if a theme has genuinely mixed signals, report it as Mixed
- **Always flag churn language immediately** — even a single credible churn signal is worth surfacing
- **Never force themes from thin data** — apply the thresholds above; sparse data is better acknowledged than inflated
- **Never infer personas beyond what the source supports** — see Persona Attribution rules above
- **Always explain Action separately from Overall Sentiment** — they answer different questions and must not be conflated

---

## Reference Files

- `references/sentiment-scoring-guide.md` — scoring rubric with worked examples per source type
- `references/source-credibility-weights.md` — how to interpret and weight feedback from different sources

> Read these on demand when you need scoring guidance or source interpretation help.
