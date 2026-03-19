# PRD Anti-Patterns

Common PRD mistakes and how to avoid them.

---

## Anti-Pattern 1: The Feature List PRD

**Symptom:** The PRD is just a list of requirements with no problem statement or strategic context.

**Why it fails:** No one knows *why* these are being built. Engineering builds the wrong thing. Stakeholders question prioritization. The PM can't defend trade-offs.

**Fix:** Always lead with the problem. Every requirement should trace back to a user pain point or business goal.

---

## Anti-Pattern 2: No Evidence in the Problem Statement

**Symptom:** "We believe users have this problem." No data, no quotes, no research.

**Why it fails:** The team questions whether the problem is real. Leadership doesn't feel urgency.

**Fix:** Use synthesis outputs. Include customer quotes, analytics data, support ticket volume, or interview findings. Even one real data point is better than none.

---

## Anti-Pattern 3: Solution Too Prescriptive

**Symptom:** PRD specifies exact UI layout, copy, colors, and pixel dimensions.

**Why it fails:** Removes design collaboration. Becomes a waterfall spec. Design feels like they're just executing, not contributing.

**Fix:** Describe *what* the solution does, not *how* it looks. "Users should be able to see their top engagement drivers at a glance" — not "a 3-column grid with blue headers."

---

## Anti-Pattern 4: No Success Metrics

**Symptom:** PRD defines problem and solution but has no metrics section.

**Why it fails:** The team can never validate if the feature succeeded. "Done" has no definition.

**Fix:** Always define at least one primary metric with a current baseline and a target. If you can't, the problem statement probably needs more work.

---

## Anti-Pattern 5: Flat Out of Scope Without Phasing

**Symptom:** A simple "not building this" list with no rationale and no vision for what comes next.

**Why it fails:** Scope creep. Stakeholders expect features that were never planned. Engineering builds v1 in a way that makes v2 harder because they didn't know v2 was coming.

**Fix:** Use Phased Scope. Document v1, v2, v3+ with descriptive labels and one-line rationale for each deferral. Give Engineering the full picture so they can build v1 in a way that doesn't block the rest.

---

## Anti-Pattern 6: No Strategic Context (Even for Small Features)

**Symptom:** PRD jumps straight from problem to solution with no "why now."

**Why it fails:** Deferred items have no principled reason for being deferred. Anyone can question the prioritization and there's no answer.

**Fix:** Always include at minimum one sentence answering "why are we doing this now and not in 6 months?" Scale up to a full section for large initiatives.

---

## Anti-Pattern 7: PRD Written in Isolation

**Symptom:** PM writes the PRD alone, presents the finished doc to the team.

**Why it fails:** No buy-in. Team doesn't understand rationale. Engineering finds gaps in the user stories during sprint planning.

**Fix:** Collaborate on user stories with design and engineering. Share a draft PRD before it's "final."

---

## Anti-Pattern 8: Ticket-Level User Stories in the PRD

**Symptom:** PRD user stories have 8+ acceptance criteria, implementation details, and edge case handling.

**Why it fails:** PRDs become specs. Design and Engineering lose room to think. The Epic Builder has nothing to add.

**Fix:** Max 3–4 acceptance criteria per PRD story. Keep them at intent level. The Epic Builder decomposes these into ticket-ready stories — let it do its job.

---

## Anti-Pattern 9: Confusing PRD with Project Plan

**Symptom:** PRD includes sprint timelines, task assignments, and delivery dates.

**Why it fails:** Mixes *what to build* with *how to deliver it*. PRDs become outdated quickly when timelines shift.

**Fix:** Keep the PRD focused on problem, solution, and requirements. Use a separate Execution & Delivery document for timelines, phasing, and team responsibilities.
