# Label Mapping Guide

Complete mapping tables from synthesis output labels to the 1–5 numeric scale used in Prioritization scoring.

---

## Why This File Exists

Each synthesis skill uses its own label vocabulary. Before scoring, every label must be converted to a number on the same 1–5 scale. This file is the authoritative translation layer. When in doubt, refer here.

---

## research-synthesis → Prioritization

### Severity
| Synthesis Label | Numeric Score | Notes |
|----------------|---------------|-------|
| High | 4 | Directly impacts core workflow, pay, or compliance |
| Medium-High | 4 | Round up — downstream impact is significant |
| Medium | 3 | Friction exists, workaround available |
| Low | 2 | Minor inconvenience |
| *(not stated)* | 2 | Default to Low if severity not declared |

> Research Synthesis does not use "Critical" — the highest is High (→ 4). Reserve score 5 for Feedback Synthesis Critical sentiment or confirmed compliance/churn overrides.

### Evidence Strength
| Synthesis Label | Numeric Score | Notes |
|----------------|---------------|-------|
| Strong | 5 | Multi-participant, verbatim, cross-persona, no contradictions |
| Moderate | 3 | Some verbatim, partial cross-persona, or small sample |
| Weak | 1 | Single mention, paraphrased only, or strong contradictions |

### Research Status → Scoring Modifier
| Synthesis Label | Action |
|----------------|--------|
| Ready for Design | No penalty — proceed normally |
| Validate First | Apply `Validate before build` flag |
| Needs Scoping | Apply `Validate before build` flag + note unresolved technical questions |

### Impact Breadth — Research Themes
| Score | Label | Signal |
|-------|-------|--------|
| 5 | Very High | 8+ participants OR strong recurrence across 3+ sessions |
| 4 | High | 5–7 participants OR recurrence across 2 sessions |
| 3 | Medium | 3–4 participants |
| 2 | Low | 2 participants |
| 1 | Isolated | 1 participant (Single Mention in synthesis) |

### Insight Stability → Evidence Strength Modifier
| Stability Label | Adjustment |
|----------------|------------|
| Strong Pattern | Use declared Evidence Strength as-is |
| Emerging Pattern | Cap Evidence Strength at Moderate (3) |
| Early Signal | Cap Evidence Strength at Weak-Low (2); apply `Validate before build` flag |

---

## request-synthesis → Prioritization

### Demand → Severity Proxy
| Synthesis Label | Numeric Score | Notes |
|----------------|---------------|-------|
| High | 4 | 10+ unique accounts or strong MRR signal |
| Medium | 3 | 3–9 unique accounts or elevated by MRR |
| Low | 2 | 1–2 accounts, no deal risk |

### Discovery Readiness → Scoring Modifier
| Synthesis Label | Action |
|----------------|--------|
| Ready | No penalty — proceed normally |
| Needs More Signal | Apply `Validate before build` flag |
| Deprioritize | Apply flag — surface but rank low |
| Park | Exclude from scoring. Document in a Parked Items note. |

### Impact Breadth — Feature Requests
| Score | Label | Unique Accounts |
|-------|-------|----------------|
| 5 | Very High | 10+ unique accounts |
| 4 | High | 6–9 unique accounts |
| 3 | Medium | 3–5 unique accounts |
| 2 | Low | 1–2 accounts with elevated MRR |
| 1 | Isolated | 1 account, no MRR elevation, no deal risk |

### Revenue Impact → Override Multiplier
| Revenue Signal | Action |
|---------------|--------|
| High Revenue Impact declared | Apply revenue multiplier to final score |
| MRR Unknown | Flag — do not apply multiplier, note missing data |
| No revenue data | No adjustment |

---

## feedback-synthesis → Prioritization

### Overall Sentiment → Severity
| Synthesis Label | Numeric Score | Notes |
|----------------|---------------|-------|
| Critical | 5 | Blocking, churn risk, or compliance — also triggers override |
| Predominantly Negative | 4 | Most feedback expresses frustration or distrust |
| Mixed | 3 | Split signals — no clear majority |
| Mostly Positive | 2 | Satisfied with minor concerns |
| Predominantly Positive | 1 | Strong positive, few or no negative signals |

### Action → Scoring Modifier
| Synthesis Label | Action |
|----------------|--------|
| Act Now | No penalty — proceed normally |
| Monitor | No penalty — note for trend tracking |
| Amplify | No penalty — note positive signal |
| Inform | Low priority — rank lower, no override |

### Signals → Override Triggers
| Signal | Action in Prioritization |
|--------|------------------------|
| Churn | Trigger Override Rule 1 — auto-escalate |
| Compliance | Trigger Override Rule 2 — auto-escalate |
| Trust | Apply Risk Mitigation orientation boost if declared; otherwise note |
| Delight | Apply Growth orientation boost if declared; otherwise note |
| Viral | Surface as context note — not a scoring input |

### Impact Breadth — Feedback Themes
| Score | Label | Signal |
|-------|-------|--------|
| 5 | Very High | High volume across many distinct submitters and sources |
| 4 | High | Moderate-high volume, multiple sources |
| 3 | Medium | Moderate volume, 2–3 sources |
| 2 | Low | Low volume, 1–2 sources |
| 1 | Isolated | Sparse mentions, single source |

---

## Ambiguous Mapping Rules

- Label not in tables → default to nearest lower score, flag as `Mapping ambiguous — defaulted to [score]`
- Required field missing → apply score of 2 (Low), flag as `Field missing — defaulted to Low`
