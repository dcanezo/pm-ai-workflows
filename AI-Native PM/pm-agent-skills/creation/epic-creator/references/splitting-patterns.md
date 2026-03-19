# Epic Splitting Patterns Reference

Adapted from Richard Lawrence's Humanizing Work methodology. Use these patterns to determine how many Epics an initiative warrants and where to draw the boundaries between them. Work through patterns in order — stop when one fits.

---

## When to Split an Initiative into Multiple Epics

Before applying patterns, ask: **Does this initiative deliver more than one distinct user outcome?**
- If yes → likely multiple Epics
- If no → likely one Epic

Also check: **Would a single Epic contain more than 8 User Stories?**
- If yes → split regardless of pattern fit

---

## The 9 Splitting Patterns (In Order)

### Pattern 1: Workflow Steps
**Signal:** The initiative involves a multi-step process where each phase could deliver value independently.

**How to split:** Each Epic covers a thin end-to-end slice of the workflow, starting with the simplest case, then adding complexity.

**Example:**
- Epic 1: Basic leave request submission (employee submits, auto-approved)
- Epic 2: Single-level manager approval flow
- Epic 3: Multi-level approval with escalation rules

**Key rule:** Each Epic must cover the full workflow end-to-end, just with increasing sophistication. Do NOT split by technical layer (front-end Epic, back-end Epic).

---

### Pattern 2: Operations (CRUD)
**Signal:** The initiative uses words like "manage," "handle," or "maintain" — signaling multiple operations.

**How to split:** One Epic per major operation — Create, Read, Update, Delete.

**Example:** "Manage employee profiles" →
- Epic 1: Create and view employee profiles
- Epic 2: Edit employee profile information
- Epic 3: Deactivate and archive profiles

---

### Pattern 3: Business Rule Variations
**Signal:** The same functionality operates differently under different rules (user types, tiers, regions, conditions).

**How to split:** One Epic per distinct rule set.

**Example:** Leave approval rules differ by employment type →
- Epic 1: Leave approval for regular employees
- Epic 2: Leave approval for contractual employees
- Epic 3: Leave approval for probationary employees

---

### Pattern 4: Data Variations
**Signal:** The feature handles meaningfully different data types or structures that require different treatment.

**How to split:** Start with the most common data type; add variations as separate Epics just-in-time.

**Example:** Payslip generation →
- Epic 1: Standard monthly payslip generation
- Epic 2: Prorated payslip for mid-month hires
- Epic 3: 13th month pay computation

---

### Pattern 5: Data Entry Methods
**Signal:** The feature supports multiple input methods of varying complexity.

**How to split:** Simple input first, enhanced input later.

**Example:** Time log entry →
- Epic 1: Manual time log entry via form
- Epic 2: Biometric device integration for automatic log capture

---

### Pattern 6: Major Effort
**Signal:** One part of the initiative is significantly larger than the rest (infrastructure, core engine, etc.).

**How to split:** Build the core infrastructure first, add remaining capabilities after.

**Example:** Loan eligibility engine →
- Epic 1: Core eligibility computation engine (major effort)
- Epic 2: Add employer tier adjustments and overrides

---

### Pattern 7: Simple / Complex
**Signal:** The feature has a simple core version and several enhancement layers.

**How to split:** Core simplest version first, enhancements as separate Epics.

**Example:** Attendance dashboard →
- Epic 1: Basic attendance summary view (present, absent, late counts)
- Epic 2: Drill-down by department and date range
- Epic 3: Exportable attendance reports

---

### Pattern 8: Defer Performance
**Signal:** The feature needs to work correctly first, then be optimized for scale or speed.

**How to split:** Functional version first, performance optimization as a separate Epic.

**Example:** Payroll computation →
- Epic 1: Accurate payroll computation for all employee types
- Epic 2: Performance optimization for bulk payroll runs (1000+ employees)

---

### Pattern 9: Break Out a Spike
**Signal:** There is significant technical uncertainty that blocks proper scoping.

**How to split:** Time-box an investigation Epic first, then scope the build Epics after.

**Example:**
- Epic 1: Technical spike — evaluate biometric API integration options (2-sprint time box)
- Epic 2: Implement selected biometric integration (scoped after spike)

---

## Split Evaluation Checklist

After determining your Epic split, verify:

- ✅ Each Epic delivers observable user value independently
- ✅ Each Epic has a clear, verifiable Definition of Done
- ✅ No Epic contains more than ~8 User Stories
- ✅ Epics are vertical slices (end-to-end value), not horizontal layers (front-end / back-end)
- ✅ Did the split reveal any low-value work that could be deferred or eliminated?

---

## Common Pitfalls

**Horizontal slicing** — Splitting by technical layer instead of user value.
- ❌ Epic 1: Build API. Epic 2: Build UI.
- ✅ Epic 1: Employee can view their leave balance (requires both API + UI)

**One giant Epic** — Everything lumped together because it shares a theme.
- If your Epic has 10+ stories, apply Pattern 1 or Pattern 7 first.

**Over-splitting** — Creating Epics so granular they lose strategic meaning.
- If an Epic would only contain 1-2 stories, it's probably just a User Story, not an Epic.
