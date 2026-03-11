---
name: request-synthesis
description: "Synthesizes batches of feature requests from multiple sources (Jira, HubSpot, email, in-app forms, customer interviews) into structured, evidence-traceable demand intelligence artifacts. Use this skill when you have 10–50 raw feature requests and need to understand: what's being asked for, whether it already exists, how many clients/users are asking, and what the MRR impact is. Feeds directly into Prioritization and PRD skills. Distinct from Feedback Synthesis — this skill handles explicit asks, not problem reports."
---

# Request Synthesis

Transforms batches of raw feature requests into structured demand intelligence. Unlike Interview Synthesis (which surfaces problems users experience), this skill answers four specific questions for every request cluster:

1. **What is being asked for?** — restated as a problem-first signal, not a solution
2. **Does it already exist?** — checked against provided references or MCP-connected tools
3. **How many clients/users want it?** — counted by unique accounts, weighted by MRR
4. **What is it worth?** — MRR impact scored and flagged where data is missing

---

## Methodological Foundations

- **Problem-first reframing** — every request rewritten as *"As a [persona], I'm trying to [goal], but I can't [outcome] because [constraint]"* before clustering. Prevents solution-led grouping.
- **Demand aggregation by unique accounts** — frequency counted by unique clients/accounts, not ticket volume. One ticket tagged to 8 clients = 8 accounts affected.
- **MRR-weighted prioritization** — revenue impact can elevate or qualify frequency signals, especially for low-count enterprise requests.
- **Existence checking** — requests validated against known product capabilities before being treated as gaps.
- **Noise isolation** — unclear, duplicate, and thin requests explicitly parked rather than silently dropped.

---

## Input Handling

Accept inputs in any of these forms — handle all three gracefully:

1. **MCP-connected tools** (primary): Query Jira, HubSpot, or connected CRM/support tools directly to retrieve requests
2. **Uploaded files or pasted content** (secondary): CSV exports, Notion docs, email threads, .md or .txt files
3. **Mixed sources** (common): Combine MCP-retrieved + uploaded content — deduplicate across sources

**Also accept as optional context:**
- Product reference document (feature list, roadmap, release notes) — used for existence checks
- MRR/ARR data per account — used for revenue impact scoring
- Persona definitions — used for accurate persona tagging

**If no reference document is provided for existence checking:** flag each request's existence status as ⚠️ Unknown — cannot verify without reference.

**If MRR data is missing for an account:** flag as ⚠️ MRR Unknown and note what data would be needed.

---

## When to Use This Skill

**Use when:**
- You have 10–50 raw feature requests to process
- Stakeholders are citing individual requests and you need patterns + evidence
- You need to know if a requested feature already exists before escalating
- Before feeding into Prioritization or PRD writing

**Don't use when:**
- You have fewer than 5 requests (triage manually)
- Requests are already clustered and problem-stated (skip to Prioritization)
- Inputs are bug reports or complaints with no feature ask (use Feedback Synthesis instead)

---

## Process

### Step 1 — Ingest & Deduplicate

- Normalize all inputs to one request per entry
- Merge exact duplicates; preserve all source references (ticket IDs, account names, links)
- Note total raw items received and duplicates removed in the output header

### Step 2 — Existence Check

Before clustering, check each request against the provided reference document or MCP-connected product data:

| Status | Meaning |
|--------|---------|
| ✅ Exists | Feature already available in product |
| ⚠️ Partial | Similar capability exists but gaps remain |
| ❌ Does not exist | Confirmed gap |
| ❓ Unknown | No reference available to verify |

Route ✅ Exists items directly to the Noise/Parked section with a note — do not cluster as demand signals. These likely indicate discoverability or education gaps, not product gaps.

### Step 3 — Rewrite as Problem-First Statements

Convert each remaining request into:
> *"As a [persona], I'm trying to [goal], but I can't [outcome] because [constraint/breakdown]."*

This forces the underlying problem to surface before clustering. A request for "bulk export" becomes *"As an HR Admin, I'm trying to run payroll reconciliation, but I can't process all records efficiently because exports must be done one at a time."*

### Step 4 — Cluster into Request Signals

Group requests by shared underlying need using this decision tree:

**Two requests are the SAME signal if they share 2 or more of:**
- Same goal being blocked (what the user is trying to achieve)
- Same workflow step where the gap occurs
- Same failure mode (missing feature, wrong output, no access, etc.)

**Split into separate signals when:**
- Different personas with conflicting needs
- One is business-critical, the other is a preference
- Evidence would support different prioritization decisions

**Merge into one signal when:**
- Same root need expressed differently across sources
- Splitting would create artificial distinctions

**Cluster by:** user goal, workflow step, failure mode
**Not by:** product area, account tier, feature name mentioned

**CRITICAL — Output one numbered request signal per cluster, not one entry per theme.**
Each cluster produces exactly one entry in the Feature Requests section of the output — with all accounts that raised it listed under Affected Clients & Revenue Impact, and all source tickets listed under Sources. The overview table has one row per cluster. If 12 raw requests cluster into 4 signals, the output has 4 numbered entries — not 12, and not 4 theme sections with sub-bullets inside them.

### Step 5 — Count Demand & Score MRR Impact

**Frequency (by unique accounts):**

| Tier | Threshold |
|------|-----------|
| High | 10+ unique clients/accounts |
| Medium | 3–9 unique clients/accounts |
| Low | 1–2 unique clients/accounts |

**Critical rule:** Count unique clients/accounts, not ticket volume.
- 1 ticket tagged to 8 clients → Medium (8 accounts)
- 8 tickets from the same client → Low (1 account)

**MRR Impact Modifier:**

| MRR Impact | Action |
|-----------|--------|
| High (≥₱2.5M MRR affected) | Elevate frequency one tier |
| Medium (₱1M–₱2.5M MRR affected) | Note in evidence, maintain tier |
| Low (<₱1M MRR affected) | No adjustment |
| Unknown | Flag as ⚠️ MRR Unknown |

**Resolving frequency/MRR conflicts:**
- High frequency + Low MRR → Likely broad SMB signal, not enterprise priority
- Low frequency + High MRR → Enterprise-critical, treat as elevated
- Conflicting source signals (Support says high, Sales says low) → Document in Open Questions, don't force resolution

### Step 6 — Assign Risk & Severity

**Risk Flags:**
- 📋 **Compliance** — legal/regulatory exposure
- 💰 **Revenue risk** — directly blocking deal close or renewal
- ⚠️ **Trust** — data, privacy, or reliability concern
- **None** — standard product gap

**Severity (Triage):**
- **Critical** — blocking payroll, compliance, or active deal
- **High** — heavy manual workaround or frequent escalations
- **Medium** — friction but workable
- **Low** — preference or rare edge case

### Step 7 — Assign Signal Strength

**Worth Reviewing** (enough signal to bring to the product team):
- ≥3 unique accounts affected, OR
- ≥1 enterprise account + deal/renewal risk, OR
- High revenue impact, OR
- Compliance/revenue risk flag + ≥2 unique accounts
- Clear pattern — not ambiguous or setup-related

**Needs More Signal:**
- Only 1–2 unique accounts (unless high revenue or enterprise blocker)
- Pattern unclear — may be user error, setup issue, or one-off
- Conflicting evidence not resolved

**Low Priority:**
- Single account, no repeat signal
- Low revenue + no strategic value
- Solved by existing feature (route to Other Findings — Already Exists)
- Vague request with no problem articulated

---

## Request Signal Template

Use the Output Structure section above as the definitive format. Key field rules:

- **Existence Status**: Does Not Exist / Partial / Unknown — always checked against reference doc or MCP before treating as a gap
- **Severity**: Always label-focused — explain why it earned the label, not what the problem is (the opening paragraph covers that)
- **Affected Clients & Revenue Impact**: List each client with their ARR or MRR. Bold the combined total. Flag unknown revenue clearly.
- **Demand**: Count unique accounts, not ticket volume. High = 10+ / Medium = 3–9 / Low = 1–2
- **Revenue elevation**: If revenue impact is high, elevate demand tier and note it explicitly
- **Signal Strength**: Worth Reviewing / Needs More Signal / Low Priority
- **Urgency**: Only include when driven by a hard external factor (compliance deadline, active churn). Remove if subjective.
- **Risk Flags**: Use sub-bullets under Recommendation. Compliance / Revenue / Trust only.

## Output Structure

### Header
```
# Feature Request Synthesis — [Date]

Time Window: [start] to [end]

Total Requests Reviewed: [N]
```

### Executive Summary
A brief overview paragraph of the requests from the data provided, followed by 3–5 highlight bullets. Requests should be ordered hierarchically: 1) Demand (highest first), 2) Revenue Impact (highest first). If revenue data is unavailable, prioritize by demand. If neither is available, prioritize by severity.

### Feature Request Overview Table
```
| # | Feature Request | Affected Clients | Revenue Impact |
|---|----------------|-----------------|----------------|
```
One row per request signal, ordered by demand then revenue impact.

### Feature Requests
Each request as a numbered section using this structure:

---

## [N]. [Feature Request Name]

[1–2 sentence neutral description of the problem being raised.]

### Status: Does Not Exist / Partial / Unknown

[Brief explanation. If Partial or Unknown, note what reference was used and what gap remains.]

### Severity: Critical / High / Medium / Low

Labeled **[Severity]** — [one sentence explaining why it earned this label, focused on what makes it this severity, not restating the problem description above.]

### Affected Clients & Revenue Impact

- [Client Name] ([Revenue] ARR or MRR)
- [Client Name] ([Revenue] ARR or MRR)
- [Unknown accounts if any] (Revenue Unknown)
- **Combined: [Total] ARR/MRR+**

### Recommendation

[1–2 sentence summary of what the data shows about this request — signal strength, notable context, or constraints. Do not rank against other requests — that is for the Prioritization skill.]

- **Demand:** High / Medium / Low — [brief explanation, note if elevated by revenue or risk context]
- **Risk Flags:**
  - [Flag] — [brief explanation]
- **Urgency:** High / Medium / Low — [only include if driven by a hard external factor like a deadline or active churn risk. Remove if urgency is subjective.]
- **Signal Strength:** Worth Reviewing / Needs More Signal / Low Priority

### Open Questions

- [Question 1]
- [Question 2]

### Sources

- [Request description] ([Source] — [Account], [ID if available])

---

### Other Findings
Houses all items not included in the main request signals. Each item gets its own entry with a status:

- **Already Exists** — feature is built; note possible discoverability gap and recommend CS action
- **Revisit Later** — legitimate gap but insufficient urgency or signal for this cycle
- **Needs More Details** — something is there but not articulated well enough to act on

Each entry includes: brief description, Status, Severity (with label-focused explanation), and Affected Clients & Revenue Impact where known.

### Legend
Always include at the bottom of every output as tables:

**Status**
| Status | Definition |
|--------|------------|
| Already Exists | Feature is available in the current product version |
| Partial | Related capability exists but the specific gap remains |
| Does Not Exist | Confirmed product gap |
| Unknown | Could not be verified — no reference document available |

**Severity**
| Severity | Definition |
|----------|------------|
| Critical | Blocking payroll, compliance, or an active deal |
| High | Heavy manual workaround or frequent escalations |
| Medium | Friction but workable |
| Low | Preference or rare edge case |

**Demand**
| Demand | Definition |
|--------|------------|
| High | 10+ unique accounts requesting the same feature |
| Medium | 3–9 unique accounts requesting the same feature |
| Low | 1–2 unique accounts requesting the same feature |

**Risk Flags**
| Flag | Definition |
|------|------------|
| Compliance | Legal or regulatory exposure |
| Revenue | Blocking deal close or renewal |
| Trust | Data, privacy, or reliability concern |

**Signal Strength**
| Signal Strength | Definition |
|----------------|------------|
| Worth Reviewing | Enough signal to bring to the product team |
| Needs More Signal | Promising but needs clarification before acting |
| Low Priority | Acknowledged — no action needed this cycle |

**Other Findings Status**
| Status | Definition |
|--------|------------|
| Already Exists | Feature is built — possible discoverability gap |
| Revisit Later | Worth noting, not urgent for this cycle |
| Needs More Details | Something is there but not articulated well enough to act on |

---

## Boundary Rules

- **Never propose solutions** — signals describe problems and gaps only. Directional framing is allowed, explicit solutions are not.
- **Never count ticket volume as demand** — always count unique accounts.
- **Never silently drop unclear items** — always document in Other Findings with appropriate status.
- **Never force Signal Strength** — if evidence is thin, mark Needs More Signal and document why.
- **Always flag missing revenue data** — Revenue Unknown is better than an invented number.
- **Always flag unverified existence** — Unknown is better than assuming a gap exists.
- **Never rank requests against each other** — describe signal strength, not priority order. Prioritization is a separate skill.
- **Only include Urgency when external** — compliance deadlines and active churn risk qualify. Subjective urgency does not.

---

## Common Pitfalls

❌ Clustering by product area ("all mobile requests")
✅ Cluster by user goal ("can't complete approval workflow on mobile")

❌ Counting 10 tickets from 1 client as High demand
✅ 10 tickets from 1 client = Low demand (1 account)

❌ Ignoring a 2-account signal with high revenue impact
✅ Flag revenue elevation — Low demand + High revenue = elevated signal

❌ Treating "Add dark mode" as a request signal
✅ Park it in Other Findings — no problem articulated

❌ Assuming a requested feature doesn't exist without checking
✅ Always existence-check first; route confirmed gaps to signals, confirmed existing to Other Findings

❌ Ranking requests against each other ("this is the top priority")
✅ Describe signal strength only — let the Prioritization skill make the ranking call

❌ Producing theme sections with supporting evidence nested inside them
✅ Each cluster = one numbered request signal in the Feature Requests section with our approved structure — Status, Severity, Affected Clients & Revenue Impact, Recommendation, Open Questions, Sources

❌ Adding a Prioritization Matrix or recommended next steps ranking
✅ Signal Strength describes evidence quality only — never rank signals against each other or suggest build order

---

## Reference Files

- `references/existence-check-guide.md` — how to check against MCP tools vs. uploaded reference docs
- `references/mrr-scoring-examples.md` — worked examples of frequency + MRR elevation logic

> Read these on demand when you need worked examples or existence-checking guidance.
