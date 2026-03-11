# Output Examples

Annotated examples for Deep Dive and Executive modes. Use these as reference when producing synthesis outputs.

---

## Example A — Deep Dive Mode (Discovery, Single Interview)

**Context**: PM notes from a 45-min interview with an HR Admin about overtime filing.

---

### 1. Research Context Snapshot
- **Research phase**: Discovery
- **Input type**: PM-authored paraphrased notes (single interview)
- **Participant**: HR Admin, mid-size manufacturing company
- **Product context**: Workforce management platform, mobile OT filing feature in scope
- **Output mode**: Deep Dive

---

### 2. Data Coverage
- **Sources**: 1 interview
- **Personas**: HR Admin (1)
- **Workflows covered**: Overtime filing, policy lookup, approval routing
- **Evidence directness**: ~20% verbatim, ~70% paraphrased, ~10% interpretive
- **Coverage gaps**: No Employee or Manager perspective in this session

---

### 3. Executive Summary
1. **OT Policy Opacity** — Users cannot determine OT eligibility without leaving the filing workflow, causing abandonment and errors.
2. **Approval Routing Uncertainty** — Admins don't know who approves which OT type, creating delays and workarounds.
3. **Mobile Friction** — Filing on mobile is described as slow and error-prone, pushing users back to desktop.

---

### 4. Thematic Breakdown

#### Theme: OT Policy Opacity

**Pattern**: HR Admins lack inline access to eligibility rules, forcing them to context-switch during filing. This creates cognitive load, errors, and distrust in the system.

**Strategic Implication**: Consider surfacing eligibility criteria inline at the point of filing decision. *(Directional — not prescriptive)*

**Opportunity Statement** *(Discovery mode)*: Help HR Admins confirm OT eligibility when initiating a filing without leaving the form.

---

**Insight ID**: OTP-01
**Pain**: Cannot verify OT eligibility without navigating away from the filing screen
**Impact — Functional**: Filing is paused; user opens policy docs in a separate tab or asks a colleague
**Impact — Emotional**: Frustration, self-doubt ("Am I doing this right?"), distrust in the tool
**Current Workaround**: Keeps a printed policy cheat sheet at their desk
**Persona**: HR Admin
**Evidence**: "I always have to check the handbook because the system doesn't tell me if someone qualifies" — Interview-A
**Evidence Directness**: Verbatim
**Frequency**: 1 of 1 (single interview)
**Intensity**: High
**Severity**: High
**Importance**: High — compliance errors are a downstream risk
**Participant Diversity**: Single persona, single interview
**Temporal Signal**: None
**Insight Stability**: Early Signal
**Weighted Confidence**: Moderate (single source, but verbatim + high intensity + compliance risk)
**Risk/Opportunity Flags**: 📋 Compliance risk, 🔁 Shadow system (printed cheat sheet)
**Roadmap Alignment**: Not currently on roadmap
⚠️ Assumption: Compliance risk inference is analytical — not stated by participant directly

---

### 5. Quantitative Signal Table

| Insight | Mentions | Intensity | Severity | Importance | Confidence | Stability |
|---------|----------|-----------|----------|------------|------------|-----------|
| OTP-01: Policy opacity | 1/1 | High | High | High | Moderate | Early Signal |
| AR-01: Approval routing unclear | 1/1 | Medium | Medium | High | Weak | Early Signal |
| MF-01: Mobile filing friction | 1/1 | Medium | Low | Medium | Weak | Early Signal |

---

### 6. Risk & Opportunity Radar

**Risk Flags**
- 📋 **Compliance risk**: OTP-01 — filing errors due to policy ambiguity could result in incorrect OT payments
- 🔁 **Shadow system**: Printed policy cheat sheet indicates the product is not trusted as the source of truth

**Opportunity Flags**
- 💰 **Revenue signal**: Inline policy guidance could differentiate platform vs. competitors who also lack this
- **Roadmap Alignment Signals**:
  - Confirms: Mobile filing is in scope ✓
  - Challenges: None identified yet
  - Absent from roadmap: Inline eligibility guidance, approval routing transparency

---

### 7. Contradictions & Unresolved Signals

No contradictions in this single-interview session.

---

### 8. Research Gaps & Next Validation Steps

1. Validate whether OT policy opacity is consistent across HR Admin persona by [conducting 3–4 additional discovery interviews] with [HR Admins at different company sizes]
2. Validate whether approval routing confusion is role-specific or systemic by [mapping approval workflows] with [HR Admins + Managers in the same org]
3. Validate whether mobile friction is device-specific or universal by [usability testing] with [HR Admins on Android vs iOS]

⚠️ Assumption to validate: Compliance risk from filing errors — confirm with [legal/compliance stakeholder interview]

---

### 9. Traceability Map

| Insight ID | Source |
|------------|--------|
| OTP-01 | Interview-A |
| AR-01 | Interview-A |
| MF-01 | Interview-A |

---
---

## Example B — Executive Mode (Post-Launch, Multi-Interview)

**Context**: 5 interviews post-launch of new mobile OT filing feature.

---

### 1. Research Context Snapshot
- **Research phase**: Post-Launch
- **Input type**: PM-authored notes (5 interviews)
- **Participants**: 3 HR Admins, 2 Employees
- **Output mode**: Executive

---

### 3. Executive Summary *(Executive mode — sections 4 and 9 suppressed)*

1. **Mobile performance below expectations** — 4 of 5 participants report filing as slower on mobile than desktop. Strong pattern.
2. **Approval status visibility gap** — 3 of 5 participants don't know where their filed OT request stands. Emerging pattern.
3. **Positive: simplified form** — 3 of 5 praised the new form layout as clearer than previous version. Emerging pattern.

---

### 5. Quantitative Signal Table

| Insight | Mentions | Intensity | Severity | Importance | Confidence | Stability |
|---------|----------|-----------|----------|------------|------------|-----------|
| Mobile performance | 4/5 | High | High | High | Strong | Strong Pattern |
| Approval status visibility | 3/5 | Medium | Medium | High | Moderate | Emerging Pattern |
| Form clarity (positive) | 3/5 | Medium | N/A | Medium | Moderate | Emerging Pattern |
| Notification timing | 1/5 | Low | Low | Low | Weak | Early Signal |

---

### 6. Risk & Opportunity Radar

**Risk Flags**
- 🚨 **Churn signal**: 2 HR Admins stated they may revert to desktop-only filing if mobile doesn't improve
- ⚠️ **Trust erosion**: Approval status gap is creating anxiety — "I file and then have no idea what happens"

**Opportunity Flags**
- 🚀 **Adoption**: Form clarity improvement is being shared peer-to-peer — unprompted advocacy signal

**Roadmap Alignment Signals**
- Confirms: Form redesign was the right call ✓
- Challenges: Mobile performance was assumed resolved in QA — field data contradicts this
- Absent from roadmap: Real-time approval status tracking

---

### 7. Contradictions & Unresolved Signals

**Mobile performance split**: 4 of 5 report slowness; 1 Employee reports no issues.
⚠️ Assumption: Performance variation may be device or network-dependent (not yet validated). Recommend device/OS breakdown analysis before drawing conclusions.

---

### 8. Research Gaps & Next Validation Steps

1. Validate whether mobile slowness is device-specific by [analyzing session performance data] segmented by [device OS and model]
2. Validate whether approval status anxiety leads to duplicate filings by [querying duplicate submission rate] in [post-launch analytics]
3. Validate peer advocacy signal by [measuring referral or organic adoption rate] over [next 30 days]
