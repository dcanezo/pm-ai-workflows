# Scoring Worked Examples

End-to-end scoring examples showing all four layers applied to real inputs.

---

## Example A — Single Input (Request Synthesis Only)

**Item:** Bulk Export Feature — Demand: High (12 accounts), Revenue: ₱18M ARR, Readiness: Ready
**Orientation:** Growth | **Focus:** Enterprise expansion | **OKR:** Increase enterprise ARR 30%

- Severity: 4, Impact Breadth: 5, Evidence Strength: 3
- Base: (4×0.40)+(5×0.35)+(3×0.25) = **4.10**
- Growth orientation +20% → 4.92
- Strategic Focus +20% → 5.90
- OKR boost +10% → 6.49
- Revenue multiplier +10% → **7.14**
- **Confidence: Low** — `Single source`

---

## Example B — Two Inputs (Research + Feedback)

**Item:** Mobile Clock-In Reliability
- Research: Severity High, Evidence Strong, 6 participants, 3 sessions
- Feedback: Sentiment Critical, Signals: Churn + Trust

- Severity: 5 (Critical from feedback), Impact Breadth: 4, Evidence Strength: 5
- Base: (5×0.40)+(4×0.35)+(5×0.25) = **4.65**
- Risk Mitigation +20% → 5.58 | Focus +20% → 6.70 | CSF +15% → 7.70 | OKR +10% → **8.47**
- Churn signal → **Override: Churn applied**
- **Confidence: High**

---

## Example C — Tie Handling

Item A: 4.82 | Item B: 4.79 — difference 0.6%, within 5% threshold.

> "Items A and B score within 1% of each other — forcing a ranking would be false precision. Dashboard Performance is a defensive play (reduce friction). Bulk Notification is a growth play (expand utility). Recommend surfacing both as a strategic tradeoff."

**Flag:** `Tie — strategic tradeoff surfaced`

---

## Example D — Validation Gate

**Item:** Data Export Corruption — single CS note
- Severity: 5, Impact Breadth: 1, Evidence Strength: 1
- Base: (5×0.40)+(1×0.35)+(1×0.25) = **2.60**
- No churn, no compliance → Rule 4 applies
- **Flag:** `Validate before build — High Severity + Low Evidence`

---

## Example E — Human Override

**Original #1:** Mobile Clock-In Reliability (5.45, Override: Churn)

**PM input:** "Leadership committed Bulk Payroll Export to SunGroup Holdings as part of their renewal — decided in an exec meeting last week, not in any synthesis file."

**Action:** Apply PM Override — executive renewal commitment not captured in references. Elevate Bulk Payroll Export to #1.

**Audit note:**
> *"Ranking adjusted based on PM input: Executive commitment made to SunGroup Holdings as part of renewal agreement — not captured in synthesis references. Original data-driven recommendation was Mobile Clock-In Reliability (Score: 5.45, Override: Churn). Mobile Clock-In Reliability remains #2 and should be addressed immediately after."*

---

## Example F — Framework Translation (MoSCoW)

**Unified Ranking input:**
1. Mobile Clock-In Reliability — High, Override: Churn
2. Bulk Payroll Export — Medium, no flags
3. Slow Load Times — Medium, Monitor
4. Approval Routing Transparency — Low, Validate before build
5. Dark Mode — Low, OKR misaligned

**MoSCoW output:**
```
Must:   Mobile Clock-In Reliability — active churn risk, non-negotiable this cycle
Should: Bulk Payroll Export — strong evidence, high revenue impact, no blocking flags
Could:  Slow Load Times — real signal, monitor for escalation before committing
Could:  Approval Routing Transparency — needs validation sprint before design capacity committed
Won't:  Dark Mode — no OKR alignment this cycle, revisit if strategic focus shifts
```

---

## Example G — Unstructured Input Detection

**PM provides:** A Notion page with raw interview notes — no Severity, Evidence Strength, or Research Status fields.

**Skill response:**
> "This input doesn't appear to be a synthesis output. To prioritize reliably, the data needs to be processed through a synthesis skill first. Based on what I can see, this looks like raw research or interview notes — I'd recommend running **research-synthesis** first, then bringing the output back here to prioritize.
>
> Would you like to proceed with synthesis first, or do you have a synthesis output available?"

**If PM confirms they want to proceed anyway:**
All items flagged as `Unstructured input — confidence limited`. Tier 2 warnings applied throughout output.

---

## Example H — Tier 2 Warning (Multiple Missing Fields)

**Item:** Dashboard Redesign — from feedback-synthesis output
- Overall Sentiment: not stated
- Action: not stated
- Signals: not stated
- Volume: Moderate

**Mapping:**
- Severity: field missing → default 2, flag `Field missing — defaulted to Low`
- Action: field missing → note only
- Signals: field missing → no override triggered
- Impact Breadth: Moderate volume → 3

**Output warning surfaced:**
> `Low confidence — multiple fields missing on Dashboard Redesign. Scoring based on defaults. Validate before relying on this item's ranking.`
