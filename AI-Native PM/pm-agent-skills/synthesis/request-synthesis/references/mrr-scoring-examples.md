# MRR Scoring Examples

Worked examples for demand counting and MRR elevation logic.

---

## Core Rule: Count Unique Accounts, Not Tickets

| Scenario | Accounts | Demand |
|----------|----------|-----------|
| 1 ticket tagged to 8 clients | 8 | Medium |
| 8 tickets all from 1 client | 1 | Low |
| 3 tickets: clients A, B, C | 3 | Medium |
| 5 tickets: 2 from A, 3 from B | 2 | Low |
| 12 tickets across 11 clients | 11 | High |

---

## MRR Elevation Logic

| Client Count | Revenue Impact | Final Demand | Reasoning |
|-------------|------------|-----------------|-----------|
| 11 accounts | ₱4.25M MRR | **High** | High by count; MRR confirms |
| 2 accounts | ₱20M ARR | **Medium** | Low by count, elevated by MRR |
| 8 accounts | ₱600K MRR | **Medium** | Medium by count; low MRR, no elevation |
| 1 account | ₱10M ARR | **Medium** | Low by count, elevated by high MRR |
| 12 accounts | ₱750K MRR | **High** | High by count prevails; low MRR doesn't reduce |
| 3 accounts | ⚠️ Unknown | **Medium** | Count-based only; flag MRR Unknown |

---

## Conflict Resolution Examples

**Scenario: Support says urgent, Sales says low impact**
- Support: 6 tickets across 4 accounts — Medium demand
- Sales: "Not mentioned in any active deals"
- Resolution: Document conflict in Open Questions. Possible tier split (SMB support volume vs. Enterprise deal criteria). Don't force resolution — flag for validation.

**Scenario: High ticket volume, single account**
- 15 tickets, all from one enterprise client (₱9M ARR)
- Unique accounts: 1 → Low by count
- MRR: ₱750K MRR (₱9M ARR / 12) → High Revenue Impact → elevate to Medium
- Final: **Medium demand** — single loud account, but revenue-significant

**Scenario: Low count, enterprise deal blocker**
- 2 accounts, ₱0 MRR data available
- But Sales flags: "Active ₱12.5M ARR deal blocked on this"
- Route as **Ready** — enterprise deal blocker overrides low count threshold
- Flag: ⚠️ MRR Unknown but deal risk documented

---

## Discovery Readiness Quick Reference

| Condition | Readiness |
|-----------|-----------|
| ≥3 unique accounts | Ready |
| 1–2 accounts + enterprise deal risk | Ready |
| ≥₱2.5M MRR affected | Ready |
| Compliance/revenue flag + ≥2 accounts | Ready |
| 1–2 accounts, no deal risk, unknown MRR | Needs More Signal |
| 1 account, no repeat, low MRR | Deprioritize |
| Vague request, no problem articulated | Deprioritize |
| Feature already exists | Park → Section 3 |
