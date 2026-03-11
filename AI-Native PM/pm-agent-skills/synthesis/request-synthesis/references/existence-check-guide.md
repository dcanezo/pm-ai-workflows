# Existence Check Guide

How to verify whether a requested feature already exists before treating it as a product gap.

---

## Priority Order for Existence Checks

Always attempt in this order:

1. **MCP-connected tools** — query Jira, HubSpot, or connected product documentation directly
2. **Uploaded reference document** — check against provided feature list, release notes, or roadmap
3. **Neither available** — flag as ❓ Unknown and note what reference would be needed

---

## How to Check via MCP

If connected to Jira or a product wiki via MCP:
- Search for the core capability being requested (not the exact phrasing)
- Check both shipped features AND items already on the roadmap
- If found on roadmap but not yet shipped, status = ⚠️ Partial (planned, not available)

---

## How to Check via Uploaded Reference Doc

Scan for:
- The core user goal (not the feature name the requester used)
- Synonyms and adjacent capabilities
- Recent release notes that may have shipped this capability

**Example:**
Request: "Can we get bulk employee export?"
Search reference for: export, bulk, batch, download, CSV, all records
→ If "Export All" button is documented → ✅ Exists
→ If only individual export is documented → ❌ Does not exist
→ If batch export is listed as "Coming Q3" → ⚠️ Partial

---

## Status Definitions

| Status | When to use |
|--------|------------|
| ✅ Exists | Capability confirmed in reference or MCP. Route to Section 3 (Parked) with discoverability note. |
| ⚠️ Partial | Related capability exists but the specific gap remains. Keep as signal, note what's missing. |
| ❌ Does not exist | Confirmed gap after checking reference. Proceed to clustering. |
| ❓ Unknown | No reference available. Flag and proceed to clustering — but note confidence is lower. |

---

## Discoverability vs. Product Gap

When status = ✅ Exists, ask: **why are users requesting something that already exists?**

Possible reasons:
- Feature is buried in navigation
- Feature name doesn't match what users call it
- Feature exists on web but not mobile (partial parity gap)
- Users were never trained on it

Route these to the **→ Customer Success / Sales** handoff note, not engineering. The fix may be documentation, onboarding, or UI discoverability — not a new feature.
