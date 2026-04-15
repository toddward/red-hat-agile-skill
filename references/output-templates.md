# Output Templates

Complete templates for the final agile project plan deliverable. Use these when
assembling the output from all three phases.

---

## Intrinsic Value Framework (Detailed)

Intrinsic value is the worth an item delivers independently — even if no other item
in the plan existed. It answers "why does this matter on its own?" rather than
"how does this contribute to the larger goal?"

### Why Intrinsic Value Matters for Agile

Without intrinsic value, agile degrades into a feature factory: teams build what's
on the list without understanding why, can't make trade-off decisions during sprints,
and stakeholders can't meaningfully prioritize. When every item has articulated
intrinsic value, the team can:

- **Re-prioritize on the fly** — if priorities shift, you know which items still matter
- **Make scope cuts without panic** — you can identify the MVP subset instantly
- **Explain "why" to stakeholders** — each item justifies its own existence
- **Motivate the team** — people do better work when they understand the impact

### Value Dimensions

| Dimension | What It Captures | Signal Words | Example |
|-----------|-----------------|-------------|---------|
| **User Impact** | Direct, tangible benefit to end users | "Users can...", "Reduces user...", "Enables users to..." | "Users can reset passwords without calling support, recovering access in <2 minutes instead of 24 hours" |
| **Business Impact** | Revenue, cost reduction, compliance, market position | "Reduces cost...", "Enables revenue...", "Achieves compliance..." | "Eliminates ~150 support tickets/month at $12/ticket = ~$1,800/month savings" |
| **Technical Impact** | Capability, quality, maintainability, performance | "Establishes...", "Enables...", "Improves..." | "Establishes the authentication foundation that all role-based features depend on" |
| **Learning Impact** | Uncertainty reduced, knowledge gained, risk validated | "Validates...", "Proves...", "Determines..." | "Validates that our SSO approach works with the customer's IdP before committing to the full integration" |

### Value by Item Level

**Epic-Level Value** (Strategic)
- Answers: "Why does this capability matter to the business?"
- Should connect to business objectives or user segments
- Example: "Secure User Identity — Enables the organization to serve authenticated users,
  unlocking all personalized features and meeting regulatory requirements for data access control."

**Story-Level Value** (Tactical)
- Answers: "What specific benefit does shipping this story deliver?"
- Should be concrete enough that you could demo it to a stakeholder
- Must hold up independently: "If we shipped ONLY this story, would someone benefit?"
- Example: "Password Reset Flow — Users locked out of their account can self-recover
  within 2 minutes, eliminating the #1 support ticket category."

**Task-Level Value** (Operational)
- Answers: "Why is this work necessary?"
- Can reference parent story's value when no independent value exists
- Should still articulate the connection: "Enables X by doing Y"
- Example: "Create user_credentials table migration — Enables the authentication
  system by establishing the schema for secure credential storage."

### Writing Good Value Statements

**The Sniff Test:** Read the value statement out loud. If it sounds like it could apply
to any project ("improves user experience", "adds functionality", "enhances the system"),
it's too vague. Rewrite with specifics.

| Vague (fails sniff test) | Specific (passes) |
|--------------------------|-------------------|
| "Improves user experience" | "Reduces checkout time from 5 steps to 2, decreasing cart abandonment" |
| "Adds important functionality" | "Customers can track orders in real-time, reducing 'where's my order?' calls by ~40%" |
| "Technical improvement" | "Migrates from polling to WebSockets, reducing server load by 60% and enabling real-time features" |
| "Reduces risk" | "Automated daily backups with verified restore process — recovery time drops from 8 hours to 30 minutes" |

---

## Definition of Done Templates

### Epic-Level DoD

Epic DoD defines what "this capability is complete" means. It's broader than story DoD
and often includes cross-cutting concerns.

```markdown
**Definition of Done — Epic: [Name]**

Functional Completeness:
- [ ] All stories in this epic are completed and accepted
- [ ] [Specific capability 1] is operational in production
- [ ] [Specific capability 2] is operational in production
- [ ] Edge cases defined in stories are handled

Quality:
- [ ] Performance: [specific metric, e.g., "P95 < 200ms under 500 concurrent users"]
- [ ] Accessibility: [standard, e.g., "WCAG 2.1 AA compliant"]
- [ ] Security: [requirement, e.g., "Passes OWASP Top 10 review"]

Operational:
- [ ] Monitoring and alerting configured for key metrics
- [ ] Runbook/playbook documented for on-call team
- [ ] Rollback procedure tested

Stakeholder:
- [ ] Demo completed with [stakeholder group]
- [ ] Documentation/training materials delivered
```

### Story-Level DoD

Story DoD defines what "this story is shippable" means. Each criterion must be
verifiable by someone who didn't write the code.

```markdown
**Definition of Done — Story [E.N]: [Title]**

Functional:
- [ ] [Specific behavior 1 — include input, action, expected output]
- [ ] [Specific behavior 2]
- [ ] [Error state 1 — what happens when X goes wrong]
- [ ] [Edge case 1 — boundary condition handled]

Quality:
- [ ] [Performance criterion if applicable — specific metric]
- [ ] [Accessibility criterion if applicable]
- [ ] [Browser/device compatibility if applicable]

Technical:
- [ ] Unit tests cover public methods ([coverage target]% line coverage)
- [ ] Integration test validates [specific flow]
- [ ] Code reviewed and approved by [N] team members
- [ ] No new security vulnerabilities introduced (scan passes)

Operational:
- [ ] Feature flag configured for gradual rollout (if applicable)
- [ ] [Deployment requirement if applicable]
```

### Task-Level DoD

Task DoD is the simplest — it's the completion criterion for the work item.

```markdown
**Task [E.N.T]: [Description]**
**DoD:** [Single specific, verifiable statement]

Examples:
- "Migration script runs successfully against staging database with 0 errors and all existing data preserved"
- "API endpoint returns 200 with correct payload for all 5 test cases in the spec; returns 400/401/404 for invalid inputs"
- "Component renders correctly at 320px, 768px, and 1440px viewports; matches approved design mockup"
- "CI pipeline passes all stages: lint, test, build, security scan"
```

---

## Complete Plan Template

Use this template to assemble the final deliverable from all three phases.

```markdown
# Agile Project Plan: [Project Name]

**Generated:** [date]
**Vision:** [1-2 sentence project vision from user]
**Target Users:** [who benefits]
**Constraints:** [key constraints in brief]

---

## Executive Summary

[3-5 sentences: what this plan delivers, how many epics/stories/tasks,
estimated total effort, recommended iteration order, and the biggest risk]

---

## Fundamental Truths

[Numbered list from the Vision Archaeologist — these are the bedrock
user needs and constraints that the entire plan is built on]

1. [Truth 1]
2. [Truth 2]
...

---

## Epic Overview

| # | Epic | Stories | Tasks | Intrinsic Value (1-line) | Size | Priority |
|---|------|---------|-------|--------------------------|------|----------|

### Dependency Graph
[Visual or textual representation of epic-level dependencies]

---

## Detailed Breakdown

### Epic [N]: [Name]

**Intrinsic Value:**
- User Impact: [specific]
- Business Impact: [specific]
- Technical Impact: [specific]
- Learning Impact: [specific or N/A]
**Value Summary:** [One sentence]

**Definition of Done:**
- [ ] [epic-level criterion]
- [ ] [epic-level criterion]
...

**Fundamental Truths Addressed:** [#list]

---

#### Story [E.N]: [Title]

**Description:** [user story format or clear description]

**Intrinsic Value:**
- User Impact: [specific or N/A]
- Business Impact: [specific or N/A]
- Technical Impact: [specific or N/A]
- Learning Impact: [specific or N/A]
**Value Summary:** [One sentence]

**Definition of Done:**
- [ ] [specific, verifiable criterion]
- [ ] [specific, verifiable criterion]
...

**Size:** [S/M/L]
**Dependencies:** [story IDs or "Independent"]

**Tasks:**

| # | Task | Why Necessary | DoD | Est. | Depends On |
|---|------|--------------|-----|------|-----------|
| E.N.1 | [task] | [connection to value] | [completion criterion] | [days] | [task IDs] |
| E.N.2 | [task] | [connection to value] | [completion criterion] | [days] | [task IDs] |

---

[...repeat for all stories in all epics...]

---

## Validation Summary

### Risk Register
| # | Risk | Probability | Impact | Affected Items | Mitigation | Status |
|---|------|------------|--------|---------------|-----------|--------|

### Value Map
| Item | Value Score | Effort | Value/Effort | Quadrant |
[Sorted by value/effort ratio — highest first]

### Minimum Viable Plan (MVP)
[Smallest subset of stories that delivers core value]
| Story | Cumulative Value Delivered |

### Recommended Iteration Order

**Sprint 1: [Theme]**
- Stories: [list]
- Value unlocked: [what becomes possible]
- Risks addressed: [what's validated]
- Stakeholder message: [how to frame outcomes]

**Sprint 2: [Theme]**
...

### Stakeholder Readiness
[Summary from Red Hat — organizational fit, energy, concerns]

### Confidence Assessment
| Dimension | Confidence | Key Concern |
|-----------|-----------|------------|

### Open Questions
[Questions that need answers before or during execution]

---

## Appendix: Assumption Archaeology

[The full assumption map from Phase 1 — useful for future reference
when someone asks "why didn't we include X?"]

| Stated Requirement | Fundamental Truth | Unmasked Assumption |
```

---

## Formatting Guidelines

### Consistency Rules

- Use the same numbering scheme throughout: Epic N, Story E.N, Task E.N.T
  (e.g., Epic 1, Story 1.3, Task 1.3.2)
- Every DoD item starts with a checkbox `- [ ]`
- Every value statement uses the four-dimension structure (mark N/A where applicable)
- Every dependency reference uses the item's number, not its name
- Size estimates use S/M/L for stories, hours/days for tasks

### When the Plan Is Large

For plans with more than 5 epics or 30 stories:
- Add a table of contents at the top
- Include a one-page summary before the detailed breakdown
- Consider splitting into multiple documents: overview + one per epic
- The validation summary should still be unified across all epics

### Presenting to the User

After generating the plan:
1. Present the Executive Summary and Epic Overview first
2. Ask if the high-level structure looks right before showing details
3. Offer to dive into any specific epic's stories and tasks
4. Present the Validation Summary as a decision aid, not a blocker
5. Flag the Open Questions — these need the user's input to proceed
