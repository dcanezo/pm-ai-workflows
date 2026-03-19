# Epic Splitting Guidance

Reference for Step 2 of the Epic Creator skill. Use these patterns to reason about how many Epics to generate and how to scope each one correctly.

---

## The Core Question

Before applying any pattern, ask:
> "If this Epic shipped on its own, would a user experience something meaningfully different?"

If yes → it's a valid Epic boundary.
If no → it might be a User Story, or it needs to be merged with related work.

---

## 9 Splitting Patterns (Humanizing Work)

Work through these in order when assessing how to scope or split Epics. Stop at the first pattern that applies.

### 1. Workflow Steps
Does the initiative involve a multi-step workflow where different phases deliver value independently?

**Apply when:** The initiative has a clear sequence (e.g., submit → review → approve) where each phase changes the user experience meaningfully.

**How to split:** Each Epic covers a thin end-to-end slice, not a single step. Start with the simplest complete path, then add sophistication.

**Example:**
- Epic 1: Basic leave request submission (employee submits, manager notified)
- Epic 2: Add approval workflow (manager approves/rejects, employee notified)
- Epic 3: Add delegation rules (manager can delegate approvals)

**Wrong:** Epic 1 = submission form, Epic 2 = notification system (horizontal/technical split — neither delivers full value alone)

---

### 2. Operations (CRUD)
Does the initiative involve managing something — creating, viewing, editing, deleting?

**Apply when:** The description uses words like "manage," "handle," or "maintain."

**How to split:** One Epic per major operation group, if each is large enough. Often these stay as User Stories within one Epic rather than separate Epics.

**Example:**
- Epic 1: Employee profile creation and viewing
- Epic 2: Profile editing and deactivation

---

### 3. Business Rule Variations
Does the initiative behave differently for different user types, tiers, regions, or conditions?

**Apply when:** The same feature has meaningfully different rules for different scenarios.

**How to split:** One Epic per rule variation, if each variation is complex enough to warrant it.

**Example:**
- Epic 1: Leave approval for regular employees
- Epic 2: Leave approval for probationary employees (different rules apply)

---

### 4. Data Variations
Does the initiative handle different types of data or input structures?

**Apply when:** The feature must support multiple data formats or structures that require different handling.

**How to split:** Start with the most common data type, add variations as separate Epics only if the complexity warrants it.

---

### 5. Data Entry Methods
Is there a simple version of the UI and a more sophisticated version?

**Apply when:** The core functionality can work with a basic UI first, with enhanced UX added later.

**How to split:**
- Epic 1: Core functionality with simple UI
- Epic 2: Enhanced UI/UX improvements

---

### 6. Major Effort
Is one part of the initiative significantly more complex than the rest?

**Apply when:** One capability requires building foundational infrastructure that others depend on.

**How to split:**
- Epic 1: Build the core/foundational piece
- Epic 2: Add the remaining capabilities on top

---

### 7. Simple / Complex
What's the simplest version of this feature that still delivers value?

**Apply when:** The initiative has a clear MVP version and a more complete version.

**How to split:**
- Epic 1: Core simplest version (delivers the primary value)
- Epic 2: Enhancements and edge cases

---

### 8. Defer Performance
Does the feature need to work correctly before it needs to work fast?

**Apply when:** Performance optimization is a significant effort that can be decoupled from correctness.

**How to split:**
- Epic 1: Make it work correctly
- Epic 2: Make it performant at scale

---

### 9. Break Out a Spike
Is there too much uncertainty to scope the Epics properly?

**Apply when:** The team doesn't know enough to estimate or split the work reliably.

**How to handle:** Recommend a time-boxed investigation (spike) before generating Epics. Flag this to the user.

---

## Split Evaluation

After determining the Epic split, check:

✅ **Does each Epic deliver standalone user value?**
If a user can experience something meaningfully different when one Epic ships without the others, the split is valid.

✅ **Is the Definition of Done distinct per Epic?**
Each Epic should have a unique "complete when" statement. If two Epics share the same DoD, consider merging them.

✅ **Are the Epics roughly comparable in scope?**
One Epic shouldn't be 2 days of work while another is 3 months. If sizes are wildly different, re-examine the split.

✅ **Does the split reveal any low-value work?**
Good splits sometimes surface stories or even entire Epics that aren't worth building. Flag these to the user.

---

## Anti-Patterns to Avoid

**Horizontal slicing** — splitting by technical layer instead of user value
- ❌ Epic 1: API, Epic 2: UI, Epic 3: Database
- ✅ Each Epic should touch all layers and deliver a complete user experience

**One mega-Epic** — dumping everything into a single container
- ❌ "Mobile App" Epic with 30 stories across 5 modules
- ✅ Split by distinct user experiences or capabilities

**Micro-Epics** — splitting so granularly that each Epic is just one story
- ❌ An Epic for every button or field
- ✅ Epics should contain multiple related stories

**Technical task Epics** — no user value stated
- ❌ "Refactor authentication service"
- ✅ "Authentication | SSO Login — complete when employees can log in with company credentials"
