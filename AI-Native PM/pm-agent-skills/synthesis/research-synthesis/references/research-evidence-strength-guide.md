# Confidence Scoring Rubric

## Weighted Confidence Score

The score is a composite of five factors. Evaluate each, then assign a final **Strong / Moderate / Weak** rating.

---

## Factor 1 — Frequency

How many participants mentioned this insight?

| Count | Weight |
|-------|--------|
| 4+ of N | High |
| 2–3 of N | Medium |
| 1 of N | Low |

*For single-input synthesis, frequency is always 1 — other factors carry more weight.*

---

## Factor 2 — Intensity

What language did the participant use?

| Language signals | Weight |
|-----------------|--------|
| "extremely," "always," "impossible," "broken," "I can't" | High |
| "often," "annoying," "wish it would," "takes too long" | Medium |
| "sometimes," "minor," "slightly," "not a big deal" | Low |

---

## Factor 3 — Participant Diversity

Does this insight appear across different personas, workflows, or contexts?

| Distribution | Weight |
|-------------|--------|
| Appears across 3+ distinct personas or workflows | High |
| Appears in 2 personas or contexts | Medium |
| Only one persona or one context | Low |

---

## Factor 4 — Research Phase Appropriateness

Is this the right type of signal for the stated research phase?

| Phase | High-weight signals |
|-------|-------------------|
| Discovery | Problem articulation, workarounds, emotional frustration, unmet needs |
| Validation | Reaction to concept, willingness to use, preference signals |
| Usability | Task completion difficulty, confusion points, navigation failures |
| Post-Launch | Adoption blockers, regression complaints, delight signals |

*Penalize signals that don't fit the phase — e.g., a feature preference in a discovery session is low-weight.*

---

## Factor 5 — Contradiction Factor

Is there conflicting evidence for this insight?

| Conflict level | Adjustment |
|---------------|------------|
| No contradictions | No penalty |
| Minor contradiction (1 dissenting view) | Moderate penalty — downgrade one level |
| Strong contradiction (split 50/50 or close) | Heavy penalty — flag as unresolved, cap at Moderate |

---

## Final Score Calculation

Evaluate all five factors and assign holistically:

| Final Score | Criteria |
|-------------|---------|
| **Strong** | High frequency + high intensity + cross-persona + phase-appropriate + no contradictions |
| **Moderate** | Mixed factors — some high, some medium — or minor contradictions present |
| **Weak** | Single mention, low intensity, single persona, or strong contradiction present |

---

## Worked Examples

**Example A — Strong**
> "4 of 5 HR Admins described overtime filing as 'confusing' or 'broken.' No dissenting views. Paraphrased notes, so evidence directness is moderate — final score: **Strong (evidence-moderate)**"

**Example B — Moderate**
> "2 of 4 employees mentioned difficulty on mobile. 1 said mobile works fine. Cross-persona? No — all same role. Phase-appropriate for usability? Yes. Final score: **Moderate**"

**Example C — Weak**
> "1 manager mentioned preferring a different color scheme. Single mention, low intensity ('would be nice'), single persona. Final score: **Weak**"

---

## Evidence Directness Modifier

Apply this on top of the confidence score:

| Evidence type | Modifier |
|--------------|---------|
| Verbatim quote | No adjustment |
| Paraphrased by PM | Note: "evidence-moderate" |
| PM interpretive summary | Downgrade one level + add ⚠️ Assumption label |
