# Sentiment Scoring Guide

How to score sentiment consistently across different feedback source types.

---

## Core Sentiment Scale

| Score | Label | Signal |
|-------|-------|--------|
| 😊 Positive | User is satisfied, delighted, or advocating | Praise, recommendation, compliments |
| 😐 Neutral | No strong emotional signal | Factual statements, balanced views |
| 😞 Negative | User is frustrated, disappointed, or complaining | Complaints, friction language, dissatisfaction |
| 🚨 Critical | Severe negative — action risk | Churn language, trust breach, compliance concern |

---

## Scoring by Source Type

### App Store Reviews
- Weight: **Moderate** — emotional, public, but unverified context
- Positive signals: 4–5 star reviews with specific praise
- Negative signals: 1–2 star reviews, especially with specific pain points
- Watch for: review bombing (sudden spike = likely triggered by a release)
- Ignore: reviews that are clearly about a different app or version

### NPS/CSAT Responses
- Weight: **High** — structured, intentional, tied to a known user
- NPS 9–10 = Positive, NPS 7–8 = Neutral, NPS 0–6 = Negative
- CSAT 4–5 = Positive, CSAT 3 = Neutral, CSAT 1–2 = Negative
- Always pair score with verbatim comment when available
- Watch for: low scores with no comment (signal exists but root cause unknown)

### Support Tickets
- Weight: **High** — user is actively blocked, not just opining
- All support tickets carry at least Negative baseline sentiment
- Escalated tickets = Critical
- Watch for: repeat tickets on same issue from same account = high severity

### CS/AM Notes
- Weight: **Very High** — account context is known, relationship at stake
- CS notes often contain MRR context — preserve it
- Watch for: renewal risk language, executive escalation mentions
- Churn language here = 🚨 Critical regardless of volume

### In-App Feedback Forms
- Weight: **Moderate-High** — in-context, intentional, but variable quality
- Often contains both sentiment and embedded requests
- Watch for: very short responses ("bad," "fix this") — sentiment is clear but root cause needs inference

### Social Media / Community Posts
- Weight: **Moderate** — public signal but emotional and unverified
- High engagement posts (likes, shares, comments) = 📣 Viral risk
- Watch for: posts that could go viral negatively — flag immediately regardless of overall volume
- Positive viral posts = 🌟 Delight signal worth amplifying

---

## Theme-Level Sentiment Thresholds

| Distribution | Label |
|-------------|-------|
| 70%+ positive | Predominantly Positive |
| 40–69% positive, <20% negative | Mostly Positive |
| Mixed — no clear majority | Mixed |
| 40–69% negative, <20% positive | Mostly Negative |
| 70%+ negative | Predominantly Negative |
| Any Critical signals present | Critical (regardless of overall distribution) |

---

## Worked Examples

**Example A — App Store Theme**
- 45 reviews on mobile clock-in feature
- 30 positive (5-star, "easy to use"), 10 negative (1-star, "keeps crashing"), 5 neutral
- Theme sentiment: Mostly Positive (67% positive, 22% negative, 11% neutral)
- But: 3 negative reviews mention data loss → flag ⚠️ Trust erosion

**Example B — Support Ticket Theme**
- 12 tickets about payroll export errors
- All negative by definition (users are blocked)
- 2 tickets mention "this is affecting our payroll run" → 🚨 Critical
- Theme sentiment: Critical

**Example C — Mixed Source Theme**
- NPS comments: mostly positive about new dashboard
- App store: mostly negative about same dashboard (performance issues)
- CS notes: neutral — no escalations
- Theme sentiment: Mixed — source breakdown reveals the split
- ⚠️ Assumption: App store users may be on older devices/OS versions
