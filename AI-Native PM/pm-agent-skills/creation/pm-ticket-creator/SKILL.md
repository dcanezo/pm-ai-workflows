---
name: pm-ticket-creator
description: Creates Jira-ready product management tickets (User Stories) following INVEST principles with a structured format including Mike Cohn use case framing, Problem, Solution, Gherkin UACs with scenario labels, and Features In/Out of Scope. Use when a user asks to "create a ticket", "draft a user story", "write a story", "create a story", "draft a ticket", or provides a story title from an Epic. Always use this skill when a story title is provided — even without additional context — as the skill is designed to infer what it can and ask only for what's genuinely missing.
---

# PM Ticket Creator

Creates Jira-ready User Story tickets from either a story title (handed off from Epic Creator) or a freeform request. Follows INVEST principles and outputs a structured ticket with a Mike Cohn use case statement, Problem, Solution, UACs in Gherkin format, and scope boundaries.

> This skill creates User Stories only. For Epics, use the Epic Creator skill.

---

## Step 1: Detect Input Mode

### Mode A — Story Title from Epic Creator
**Signal:** User provides a task-style story title (e.g. "Receive a push notification when a Missing Log discrepancy is recorded") with or without Epic context.

**Behavior:**
- Infer initiative tag, module, persona, and problem context from the title and any Epic context provided
- Do NOT re-ask for context already established at the Epic level
- Ask only for what is genuinely missing — typically the specific behavior details needed to write UACs

**The one question to ask in Mode A:**
> "What should happen when [key interaction]?" — focus on the specific behavior, edge cases, or conditions that aren't obvious from the title alone.

If the user provides Epic context (Problem, Solution, Definition of Done), use it directly. Do not ask them to repeat it.

### Mode B — Freeform Request (No Epic Context)
**Signal:** User describes a feature, bug fix, or improvement without a story title or Epic.

**Behavior:**
Ask only what's needed to draft the ticket:
- What feature or functionality needs to be built?
- What problem does this solve?
- Which module/area does this affect?
- Who are the primary users/personas?

If context is rich enough to infer answers, proceed directly — don't ask questions you can answer yourself.

---

## Step 2: Generate the Ticket

### Title Format
`<INITIATIVE> | <MODULE> | <SHORT DESCRIPTION>`

**Approved Initiative Tags:** VAPT, BAU, OLYMPUS ENT, OLYMPUS MVP, TECH DEBT
- Infer from context when possible
- If unclear, ask: "Which initiative does this belong to?" and provide the list

**Module**
- Infer from context keywords
- If unable to determine, ask: "Which module is this for?"

---

### Ticket Structure

**Title**
`INITIATIVE | MODULE | DESCRIPTION`

---

**Problem**

Clearly state the issue, need, or opportunity. Provide context on why it matters. Spell out acronyms on first use.

End the Problem section with the Mike Cohn use case statement, italicized:

*As a [persona], I want to [action], so that [outcome].*

> The Mike Cohn line appears once — at the end of the Problem section only. Never at the top of the ticket.

---

**Solution / Expected Results**

Describe what will be built. Focus on specific feature or functionality. Use bullets or paragraphs based on content complexity.

---

**User Acceptance Criteria**

Default to Gherkin format with scenario labels.

**Format:**

*Scenario [N]: [Human-readable scenario title]*
- **Given** that [persona or condition],
- **and Given** that [additional precondition — only if a second distinct precondition is independently necessary],
- **When** [action or trigger],
- **Then** [expected result],
- **And** [additional result — only if needed].

**Rules:**
- Every Given must start with "Given that"
- Use "and Given" only when two or more preconditions are each independently necessary and cannot be cleanly combined into one
- One **When** per scenario — if you need multiple, split into separate scenarios
- One **Then** per scenario — use **And** for additional outcomes of the same trigger
- Bold all keywords: Given, and Given, When, Then, And
- Include edge cases only when relevant to the feature

**Tables format:** Only use if user explicitly requests it or there are 6+ similar scenarios with complex data specifications.

---

**Features In / Out of Scope**

- **In-Scope:** Generate suggestions based on Problem, Solution, and UAC
- **Out-of-Scope:** Identify related features explicitly excluded
- Use simple bullet lists

---

## Step 3: INVEST Validation

Before presenting the ticket, perform a quick INVEST check:
- **I - Independent:** Can be developed without blocking dependencies?
- **N - Negotiable:** Focuses on outcomes, not implementation details?
- **V - Valuable:** Clear user/business benefit?
- **E - Estimatable:** Specific enough to estimate effort?
- **S - Specific:** Clear scope and acceptance criteria?
- **T - Testable:** Can verify completion through UAC?

If any principle is violated, flag it briefly after presenting the ticket:
> ⚠️ This ticket may not be [principle] because [brief reason]. Would you like me to revise it?

---

## Step 4: Present the Ticket

Present the ticket in markdown format with clear headers.

---

## Step 5: Post-Output Review

After presenting the ticket, automatically review the UACs and surface any of the following — without waiting to be asked:

**Redundancy check**
> ⚠️ Scenario [N] may be redundant — [brief reason]. Consider removing it or merging it into Scenario [X].

**Missing precondition check**
> 💡 Scenario [N] might be missing a precondition — [brief reason]. Consider adding an "and Given."

**Scope check**
> 💡 [Item] in the In-Scope list may belong in Out-of-Scope — [brief reason].

Only surface observations that are genuinely useful. Do not manufacture feedback for the sake of appearing thorough. If the ticket is clean, say so:
> ✅ UACs look solid — no redundancies or gaps spotted.

Then ask: "Would you like to refine any section?"

---

## Examples

### Example 1: Mode A — Story Title from Epic (Push Notification)

**User Input:** "Receive a push notification when a Missing Log discrepancy is recorded"
*(With Epic context: Resolution Center on Mobile | Missing Logs Foundation)*

**Mode A question asked:**
> "What should happen when the employee taps the notification? Any conditions where it shouldn't fire?"

**Generated Ticket:**

**Title:** BAU | Resolution Center | Receive Push Notification When a Missing Log Discrepancy is Recorded

---

**Problem**

Employees who use the Sprout HR mobile app as their primary interface have no real-time signal when a Missing Log attendance discrepancy is recorded against them. They only discover the issue at payroll time — when deductions have already been processed and the resolution window may have closed.

The mobile app currently creates a false sense of security: employees clock in and out on mobile but receive no feedback when something went wrong.

*As an employee using the Sprout HR mobile app, I want to receive a push notification when a Missing Log discrepancy is recorded, so that I can act on it immediately instead of discovering it at payroll time.*

---

**Solution / Expected Results**

Trigger a push notification to the employee's mobile device when a Missing Log discrepancy is recorded after their shift ends.

- Notification fires once per Missing Log discrepancy, triggered after shift end
- Tapping the notification deep-links the employee directly to the discrepancy detail in the Resolution Center
- Notification does not fire if the employee has already filed a Certificate of Attendance (CoA) before shift end
- Notification copy to be defined by the Product Designer

---

**User Acceptance Criteria**

*Scenario 1: Employee receives a push notification after a Missing Log is recorded*
- **Given** that I am an employee with push notifications enabled on the Sprout HR mobile app,
- **When** a Missing Log discrepancy is recorded against my attendance after my shift ends,
- **Then** I receive a push notification on my mobile device,
- **And** the notification appears exactly once for that discrepancy.

*Scenario 2: Tapping the notification redirects to the discrepancy*
- **Given** that I have received a push notification for a Missing Log discrepancy,
- **When** I tap the notification,
- **Then** I am redirected to the discrepancy detail screen in the Resolution Center.

*Scenario 3: Notification does not fire if CoA was already filed before shift end*
- **Given** that I have a Missing Log discrepancy for today's shift,
- **and Given** that I filed a Certificate of Attendance before my shift ended,
- **When** the system evaluates whether to trigger a Missing Log notification after shift end,
- **Then** no push notification is sent for that discrepancy.

---

**Features In / Out of Scope**

**In-Scope**
- Push notification trigger for Missing Log discrepancies after shift end
- One-time notification rule per discrepancy
- Deep-link from notification to discrepancy detail in Resolution Center
- Suppression logic when CoA is filed before shift end

**Out-of-Scope**
- Notification copy and design — to be defined by Product Designer
- Push notifications for discrepancy types other than Missing Logs
- In-app notification center or badge count
- Email or SMS notification fallback
- Notification behavior when push permissions are disabled

---

**Post-Output Review:**
> ✅ UACs look solid — no redundancies or gaps spotted. Scenario 3 now uses "and Given" to surface both preconditions clearly.

---

### Example 2: Mode B — Freeform Request

**User Input:** "Create a ticket for removing the 'Resend for Editing' option for Olympus MVP approvers"

**Title:** OLYMPUS MVP | Approval Center | Remove Resend for Editing for Leaves, OT, and CoA

---

**Problem**

For Olympus MVP, updating or editing submitted requests is not supported, as the required APIs to modify and resubmit requests are not yet available. Allowing Approvers to resend requests for editing under Olympus MVP leads to a broken and misleading flow where requestors cannot complete the intended action.

*As an Approver under Olympus MVP, I want to only see actions that are fully supported, so that I don't initiate a flow that cannot be completed.*

---

**Solution / Expected Results**

Remove the Resend for Editing action for Approvers when reviewing Leave, Overtime (OT), and Certificate of Attendance (CoA) requests under Olympus MVP.

- Approvers should only see actions that are fully supported end-to-end
- For Legacy: existing behavior remains unchanged

---

**User Acceptance Criteria**

*Scenario 1: Olympus MVP approver does not see Resend for Editing*
- **Given** that I am an Approver from an Olympus-enabled company reviewing a Leave, OT, or CoA request,
- **When** I view the available approval actions,
- **Then** the "Resend for Editing" option is not available,
- **And** I can only Approve or Reject the request.

*Scenario 2: Legacy approver still sees Resend for Editing*
- **Given** that I am an Approver from a Legacy company reviewing a Leave, OT, or CoA request,
- **When** I view the available approval actions,
- **Then** the "Resend for Editing" option is available.

---

**Features In / Out of Scope**

**In-Scope**
- Conditional removal of Resend for Editing for Leaves, OT, and CoA under Olympus MVP
- Preservation of existing behavior for Legacy companies

**Out-of-Scope**
- Enabling request update/edit APIs for Olympus MVP
- UI redesign beyond hiding the Resend for Editing action
- Applying this change to other request types (SA, OB, and UT)

---

**Post-Output Review:**
> ✅ UACs look solid — scenarios are distinct, non-redundant, and cover both the positive and legacy cases.

---

## Troubleshooting

### Unclear Initiative Tag
**Symptom:** Cannot determine which initiative tag applies.
**Solution:** Ask: "Which initiative does this belong to?" and provide the list: VAPT, BAU, OLYMPUS ENT, OLYMPUS MVP, TECH DEBT.

---

### Vague Problem Statement
**Symptom:** User provides minimal context like "fix the bug" or "improve the feature."
**Solution:** Ask:
- What specific bug or issue exists?
- What is the current behavior vs. expected behavior?
- Which module/area is affected?
- Who is impacted?

---

### UAC Format Uncertainty
**Symptom:** Unclear whether to use Gherkin or Tables.
**Solution:** Default to Gherkin with scenario labels. Use tables only when user explicitly requests it or there are 6+ similar scenarios with complex data specifications.

---

### Missing Persona
**Symptom:** Cannot determine user persona for Gherkin Given.
**Solution:** Infer from context (e.g., "approver", "employee", "admin"). If unclear, default to "user." If the ticket clearly involves specific roles, ask: "Who are the primary users for this feature?"
