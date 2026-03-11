# Source Credibility Weights

How to interpret and weight feedback from different sources when signals conflict.

---

## Source Hierarchy (Highest to Lowest Credibility)

| Source | Credibility | Why |
|--------|------------|-----|
| CS/AM Notes | ⭐⭐⭐⭐⭐ | Known account, relationship context, MRR known |
| Support Tickets | ⭐⭐⭐⭐ | User is actively blocked, specific problem stated |
| NPS/CSAT | ⭐⭐⭐⭐ | Structured, intentional, tied to known user |
| In-App Forms | ⭐⭐⭐ | In-context, intentional, variable quality |
| App Store Reviews | ⭐⭐ | Public, emotional, unverified context |
| Social Media | ⭐⭐ | Public signal, emotional, unverified |

---

## When Sources Conflict

**App store negative + CS notes neutral**
→ App store users may represent a vocal minority or specific device/OS issue
→ Don't elevate to Critical based on app store alone
→ Flag as Mixed, investigate with CS for account-level confirmation

**Support tickets high volume + NPS scores high**
→ Support issues may be concentrated in a specific persona or tier
→ NPS may reflect a different user segment (power users vs. casual users)
→ Break down by persona before concluding

**Social media negative + all other sources neutral**
→ Social may be amplifying a single incident or edge case
→ Check if it's a single viral post or broad signal
→ Flag 📣 Viral risk but don't elevate theme sentiment without corroboration

**CS/AM note flags churn + no other signal**
→ Treat as 🚨 Critical regardless
→ Single CS churn note outweighs 10 neutral app store reviews
→ MRR context makes this the highest-weight signal

---

## Volume vs. Credibility

High volume from low-credibility sources does not automatically outweigh low volume from high-credibility sources.

| Scenario | Interpretation |
|----------|---------------|
| 50 app store complaints, 0 support tickets | Investigate — may be visibility/discovery issue, not blocking |
| 3 support tickets, 0 app store complaints | Real blocking issue, likely narrow persona |
| 1 CS churn note, everything else positive | 🚨 Critical — act immediately |
| 100 NPS detractors, CS notes positive | Segment split — NPS may be capturing different tier |

---

## Preserving Source Context in Output

Always note the source alongside every sentiment score. Never aggregate across sources without showing the breakdown. A theme that is Predominantly Positive on NPS but Critical on support tickets is not "Mixed" — it's two different stories that need to be told separately.
