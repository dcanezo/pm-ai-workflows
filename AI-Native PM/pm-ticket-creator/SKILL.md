---
name: pm-ticket-creator
description: Creates product management tickets (user stories and epics) following INVEST principles with structured format including Problem, Solution, User Acceptance Criteria, and Features In/Out scope. Use when user asks to "create a ticket", "draft a user story", "write an epic", "create a story", "draft a ticket", or mentions ticket/story creation for product features.
---

# PM Ticket Creator

## Instructions

### Step 1: Understand the Request

Analyze the user's request to determine:
- **Ticket Type:** User Story or Epic?
- **Context Provided:** Is there enough detail to draft immediately, or do clarifying questions need to be asked?

**If context is rich (feature description, problem, personas mentioned):** Proceed to Step 2.

**If context is vague:** Ask targeted questions:
- What feature or functionality needs to be built?
- What problem does this solve?
- Which module/area does this affect?
- Who are the primary users/personas?

### Step 2: Generate the Ticket

Create a ticket following this exact structure:

#### Title Format
`<INITIATIVE> | <MODULE> | <SHORT DESCRIPTION>`

**Approved Initiative Tags:** VAPT, BAU, OLYMPUS ENT, OLYMPUS MVP, TECH DEBT
- Infer from context when possible
- If unclear, ask which initiative tag to use

**Keep titles concise and descriptive.**

#### Module
- Infer module from context keywords
- If unable to determine, ask: "Which module is this for?"

#### Body Sections (in order)

**1. Problem**
- Clearly state the issue, need, or opportunity
- Provide context on why this matters
- Spell out acronyms on first use, then use abbreviation

**2. Solution / Expected Results**
- Describe what will be built
- For Epics: Can include Key Deliverables as bullet points with sub-bullets
- For User Stories: Focus on specific feature/functionality
- Use bullets or paragraphs based on content complexity

**3. User Acceptance Criteria**

**Default: Use Gherkin format**

**Formatting Structure:**
Each scenario should use line breaks for readability:

1. **Given** that [persona or condition],

   **When** [action or condition],
   
   **Then** [expected result],
   
   **And** [additional conditions or results] (if applicable)

**Guidelines:**
- **Given** can be a persona ("I'm an Approver") OR a system condition ("a shift has overnight hours")
- **When** can be a user action ("I click the button") OR a system condition ("the break is set after midnight")
- **Then** always describes the expected result or outcome
- Include multiple scenarios using numbered lists (1., 2., 3., etc.)
- Bold the Given/When/Then/And keywords for clarity
- Include edge cases only when relevant to the feature

**Tables format:** Only use if user explicitly requests "use tables" or the ticket has complex data specifications with multiple similar scenarios (6+ scenarios)

**Tables format structure:**
When using tables, organize as:

| Scenario/Section | Condition/Field | Expected Result/Format |
|------------------|-----------------|------------------------|
| [Context]        | [Specific case] | [What should happen]   |

Adjust columns based on what's being tested (2-3 columns typical).

**4. Features In / out (scope)**
- **In-Scope:** Generate suggestions based on Problem, Solution, and UAC
- **Out-of-Scope:** Identify related features that are explicitly excluded
- Use simple bullet lists (no emojis needed)

#### Epic-Specific Structure
Epics follow the same 4-section structure but with these characteristics:
- **Problem:** High-level, strategic challenge
- **Solution / Expected Results:** Often includes Key Deliverables organized with bullets and sub-bullets
- **UAC:** High-level Gherkin format
- **Features In/Out:** Broad scope is acceptable for cohesive initiatives

### Step 3: INVEST Validation

Before presenting the ticket, perform a quick INVEST check:
- **I - Independent:** Can be developed without blocking dependencies?
- **N - Negotiable:** Focuses on outcomes, not implementation details?
- **V - Valuable:** Clear user/business benefit?
- **E - Estimatable:** Specific enough to estimate effort?
- **S - Specific:** Clear scope and acceptance criteria?
- **T - Testable:** Can verify completion through UAC?

**If any principle is violated:**
Flag it briefly: "⚠️ This ticket may not be [Specific/Testable/etc.] because [brief reason]. Would you like me to revise it?"

Keep it simple - don't overwhelm with detailed explanations unless the user asks for clarification.

### Step 4: Present and Iterate

- Present the ticket in markdown format with clear headers
- Ask: "Would you like to refine any section?"
- Allow iteration: user can request changes to specific sections

**Output Format:**
```
**Title:** <INITIATIVE> | <MODULE> | <DESCRIPTION>

**Problem**
[Problem text]

**Solution / Expected Results**
[Solution text]

**User Acceptance Criteria**
[UAC content]

**Features In / out (scope)**
[Scope content]
```

## Examples

### Example 1: User Story with Gherkin UAC

**User Request:** "Create a ticket for removing the 'Resend for Editing' option for Olympus MVP approvers"

**Generated Ticket:**

**Title:** OLYMPUS MVP | Approval Center | Remove Resend for Editing for Leaves, OT, and CoA

**Problem**

For Olympus MVP, updating or editing submitted requests is not supported, as the required APIs to modify and resubmit requests are not yet available. As a result, allowing Approvers to resend requests for editing under Olympus MVP leads to a broken and misleading flow, where requestors cannot complete the intended action.

**Solution / Expected Results**

Remove the Resend for Editing action for Approvers when reviewing Leave, Overtime (OT), and Certificate of Attendance (CoA) requests under Olympus MVP.

For Olympus MVP:
- Approvers should only see actions that are fully supported end-to-end
- Approvers should not be presented with actions that cannot be completed (Resend/Resubmit for Editing)

For Legacy:
- Existing behavior remains unchanged

This ensures a clear, honest, and functional approval experience for Olympus MVP users.

**User Acceptance Criteria**

1. **Given** that I'm an Approver from an Olympus-enabled company reviewing a Leave/OT/CoA request,

   **When** I view the available approval actions,
   
   **Then** the "Resend for Editing" option should NOT be available,
   
   **And** I should only be able to Approve or Reject the request.

2. **Given** that I'm an Approver from a Legacy company reviewing a Leave/OT/CoA request,

   **When** I view the available approval actions,
   
   **Then** the "Resend for Editing" option should be available.

**Features In / out (scope)**

**In-Scope**
1. Conditional removal of Resend for Editing for Leaves, Overtime, and Certificate of Attendance requests under Olympus MVP
2. Preservation of existing behavior for Legacy companies

**Out-of-Scope**
1. Enabling request update/edit APIs for Olympus MVP
2. UI redesign beyond hiding the Resend for Editing action
3. Applying this change to other request types (SA, OB, and UT)

---

### Example 2: Epic

**User Request:** "Create an epic for establishing the Pulse infrastructure and data foundations"

**Generated Ticket:**

**Title:** Pulse | Core Infrastructure & Data Foundations | Epic 0

**Problem**

Pulse requires a secure, scalable, and HRIS (Human Resources Information System)-native infrastructure before any user-facing features can be developed. Currently, no dedicated backend exists to handle Pulse-specific survey data, employee attributes, or anonymity logic within Sprout HR.

Without these foundations, the team cannot build or test survey creation, response submission, or analytics functionalities. Attempting to design or deliver front-end features without a defined schema, stable APIs, and clear data flow would lead to rework, performance issues, and privacy risks.

**Solution / Expected Results**

Establish the core system architecture and data models that enable Pulse to operate as a fully integrated module inside Sprout HR.

**Key Deliverables**

• **Database & Schema Setup**
  ○ Create Pulse-specific tables for surveys, questions, responses, and analytics summaries.
  ○ Implement referential links to HRIS employee data while preserving anonymity.

• **API Foundations**
  ○ Build secure REST endpoints for survey CRUD (Create, Read, Update, Delete) operations and response submission.
  ○ Define standard contracts for front-end and analytics consumption.

• **Anonymity & Privacy Logic**
  ○ Embed rules ensuring responses are non-attributable to individual employees.
  ○ Comply with PH Data Privacy Act and ISO 27001 standards.

• **Authentication & Access Control**
  ○ Enable SSO (Single Sign-On) via Sprout HR session tokens and enforce role-based access.

• **Performance & Scalability Setup**
  ○ Optimize for <2 s average API response time and scalable data handling for large clients.

• **Environment & QA Readiness**
  ○ Configure staging and production environments with seed data for QA testing.

**User Acceptance Criteria**

**Given** that Pulse is the MVP (Minimum Viable Product) phase of Project Olympus,

**When** the infrastructure is established,

**Then** the backend APIs should be stable and functional, allowing front-end teams to begin building survey and analytics features with consistent, tested endpoints.

**Features In / out (scope)**

**In-Scope**
- Database schema and table creation for Pulse
- REST API endpoints for core operations
- Anonymity and privacy rule implementation
- SSO integration and RBAC (Role-Based Access Control) enforcement
- Performance optimization for scalability
- QA environment setup with test data

**Out-of-Scope**
- Front-end UI development for surveys
- Advanced analytics or reporting dashboards
- Integration with external survey platforms
- Employee notification systems for survey launches

## Troubleshooting

### Issue: Unclear Initiative Tag

**Symptom:** Cannot determine which initiative tag (VAPT, BAU, OLYMPUS ENT, OLYMPUS MVP, TECH DEBT) applies.

**Solution:** Ask the user: "Which initiative does this belong to?" and provide the list of approved tags.

---

### Issue: Vague Problem Statement

**Symptom:** User provides minimal context like "fix the bug" or "improve the feature."

**Solution:** Ask targeted clarifying questions:
- What specific bug or issue exists?
- What is the current behavior vs. expected behavior?
- Which module/area is affected?
- Who is impacted (which user personas)?

---

### Issue: UAC Format Uncertainty

**Symptom:** Unclear whether to use Gherkin or Tables for User Acceptance Criteria.

**Solution:** 
- **Default to Gherkin** unless user explicitly requests tables
- Use Tables only when:
  - User says "use tables for UAC"
  - Multiple similar scenarios with data specifications (6+ scenarios)
  - Complex field/format requirements need documentation

---

### Issue: INVEST Validation

After generating the ticket, perform a quick INVEST check:
- **I - Independent:** Can be developed without blocking dependencies?
- **N - Negotiable:** Focuses on outcomes, not implementation details?
- **V - Valuable:** Clear user/business benefit?
- **E - Estimatable:** Specific enough to estimate effort?
- **S - Specific:** Clear scope and acceptance criteria?
- **T - Testable:** Can verify completion through UAC?

**If any principle is violated:**
Flag it briefly: "⚠️ This ticket may not be [Specific/Testable/etc.] because [brief reason]. Would you like me to revise it?"

Keep it simple - don't overwhelm with detailed explanations unless the user asks for clarification.

---

### Issue: Epic vs User Story Confusion

**Symptom:** Unclear whether request should be an Epic or User Story.

**Guidelines:**
- **Epic:** High-level initiative spanning multiple sprints, foundational work, or grouping multiple related features
  - Example: "Build payment infrastructure"
- **User Story:** Specific, actionable feature that can be completed in 1-2 sprints
  - Example: "Add credit card payment option"

**When in doubt:** Ask the user: "Should this be a high-level Epic or a specific User Story?"

---

### Issue: Scope Too Broad

**Symptom:** Features In-Scope section contains too many items or spans multiple modules.

**Solution:** 
- Suggest breaking into multiple tickets
- Ask: "Would you like to split this into separate tickets for each module/feature?"
- For Epics: Broad scope is acceptable if it represents a cohesive initiative

---

### Issue: Missing Persona

**Symptom:** Cannot determine user persona for UAC Gherkin format.

**Solution:**
- Try to infer from context (e.g., "approver", "employee", "admin")
- If unclear, default to "user"
- If ticket clearly involves specific roles, ask: "Who are the primary users for this feature?"