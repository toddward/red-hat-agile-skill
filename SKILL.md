---
name: red-hat-agile-skill
description: >
  Generate structured agile project plans with Epics, Stories, and Tasks — each with
  Definition of Done and intrinsic value statements. Uses thinking frameworks (First Principles,
  Dialectical, Six Hats) as multi-agent teams to ensure plans are grounded in real user needs
  rather than inherited assumptions. Use this skill whenever the user asks to create a project
  plan, break down a project into epics and stories, generate a backlog, plan a sprint,
  decompose requirements into agile artifacts, or wants to understand the value of their work
  items. Also trigger when users say things like "plan this project", "create stories for",
  "break this into tasks", "what epics do we need", "build me a backlog", or "help me plan
  this feature". Even if the user doesn't explicitly say "agile" — if they're asking for
  structured work decomposition with clear deliverables, this skill applies.
---

# Red Hat Agile Skill

Generate rigorous agile project plans where every item — Epic, Story, Task — has a clear
Definition of Done and an articulated intrinsic value. The process uses structured thinking
frameworks to ensure the plan is grounded in real needs, not inherited assumptions or
wishful thinking.

## Why This Exists

Most agile plans fail in one of three ways:
1. **Assumption inheritance** — Stories decompose what was asked for, not what's actually needed
2. **Missing "done"** — Teams argue about completeness because DoD was vague or absent
3. **No independent value** — Items only make sense as part of a chain, making prioritization impossible

This skill addresses all three by running the project vision through structured thinking
before any decomposition begins.

## Process Overview

Three phases, each using a different thinking framework adapted for agile planning:

```
Project Vision
      |
      v
Phase 1: DISCOVERY (First Principles)
  Strip to fundamental truths → Build epic structure from bedrock
      |
      v
Phase 2: ELABORATION (Dialectical per Epic)
  Advocate story breakdown → Challenge completeness → Integrate with DoD + value
      |
      v
Phase 3: VALIDATION (Six Hats — abbreviated)
  Facts → Risks → Value → Gut check → Final plan
      |
      v
Agile Project Plan
  Epics > Stories > Tasks
  Each with DoD + Intrinsic Value
```

---

## Before You Begin

### Gather Context

Before running the frameworks, collect this from the user (ask if not provided):

1. **Project Vision** — What are we building and why? (1-3 sentences is fine)
2. **Target Users** — Who benefits from this?
3. **Known Constraints** — Budget, timeline, technology, regulatory, team size
4. **Success Criteria** — How will we know this project succeeded?
5. **Existing Context** — Any prior work, documents, or decisions already made

If the user gives you a brief prompt like "plan a customer portal", that's enough to start —
use the Discovery phase to flesh out the rest. Don't block on having perfect inputs.

---

## Phase 1: Discovery (First Principles)

**Goal:** Strip the project vision to fundamental user needs and business truths, then
build an epic structure from only those truths.

**Why this matters:** If you skip this and jump straight to "what epics do we need?",
you'll inherit every assumption baked into the original description. First Principles
forces you to ask "what do users actually need?" before "what should we build?"

Read `references/discovery-agents.md` for agent prompts and orchestration.

### Agent Chain

```
Project Vision + Constraints
        |
        v
  Vision Archaeologist → Fundamental truths + assumption map
        |
        | truths ONLY (no original vision description)
        v
  Scope Architect → Epic structure from bedrock truths
        |
        | both original + reconstruction
        v
  Coverage Evaluator → Validated epic list with gap analysis
```

### Information Barrier (Critical)

The Scope Architect must NOT see the original project vision or description. It receives
ONLY the fundamental truths from the Archaeologist. This prevents anchoring — the epic
structure should emerge from user needs, not from how the project was described.

### Phase 1 Output

A validated list of Epics, each with:
- A clear scope boundary
- The fundamental truths it addresses
- A preliminary intrinsic value statement

---

## Phase 2: Elaboration (Dialectical per Epic)

**Goal:** For each Epic, generate Stories and Tasks through structured debate. Each item
gets a Definition of Done and intrinsic value statement.

**Why this matters:** A single pass at story decomposition tends to produce either too-thin
slices (tasks disguised as stories) or too-thick slices (epics disguised as stories). The
dialectical process catches both failure modes.

Read `references/decomposition-agents.md` for agent prompts and orchestration.

### Agent Chain (runs once per Epic)

```
Epic Definition + Fundamental Truths
        |
        v
  Story Advocate → Proposed stories with DoD + value
        |
        v
  Story Challenger → Critique: INVEST violations, DoD gaps, value gaps
        |
        v
  Story Integrator → Final stories with refined DoD + intrinsic value
        |
        v
  Task Decomposition → Tasks per story with DoD
```

### INVEST Criteria (enforced by the Challenger)

Every Story must be:
- **I**ndependent — deliverable without requiring other stories to be done first
- **N**egotiable — describes the what, not the how
- **V**aluable — delivers intrinsic value (see Value Framework below)
- **E**stimable — team can reasonably estimate effort
- **S**mall — completable within a single sprint
- **T**estable — DoD is verifiable and unambiguous

### Phase 2 Output

For each Epic:
- Stories with DoD and intrinsic value
- Tasks per story with DoD
- Dependency map (which stories/tasks block others)

---

## Phase 3: Validation (Six Hats — Abbreviated)

**Goal:** Stress-test the complete plan from four perspectives before delivering it.

**Why this matters:** Phases 1 and 2 focus on structure and correctness. Phase 3 asks
"will this actually work in the real world?" — surfacing risks, confirming value, and
checking stakeholder readiness.

Read `references/validation-agents.md` for agent prompts and orchestration.

### Agent Chain

```
Complete Plan (Epics + Stories + Tasks)
        |
        v
  White Hat → Completeness check: gaps, missing requirements, data quality
        |
        v
  Black Hat → Risk assessment: what threatens this plan?
        |
        v
  Yellow Hat → Value validation: does the total value justify the effort?
        |
        v
  Red Hat → Stakeholder gut check: will the org accept this?
        |
        v
  Blue Hat → Synthesis: final adjustments + delivery recommendation
```

### Phase 3 Output

- Risk register with mitigations
- Value summary (total intrinsic value across all items)
- Stakeholder readiness assessment
- Recommended iteration order (which epics/stories to tackle first)

---

## Intrinsic Value Framework

Every Epic, Story, and Task should articulate its intrinsic value — the worth it delivers
independently, even if no other item in the plan existed.

Read `references/output-templates.md` for the full value framework and templates.

### Value Dimensions

| Dimension | Question It Answers | Example |
|-----------|-------------------|---------|
| **User Impact** | How does this directly improve a user's life? | "Users can reset passwords without calling support" |
| **Business Impact** | What business outcome does this enable? | "Reduces support tickets by ~30%" |
| **Technical Impact** | What capability or quality does this create? | "Establishes the authentication foundation other features build on" |
| **Learning Impact** | What uncertainty does this reduce? | "Validates that our SSO integration approach works with the customer's IdP" |

### Value Levels by Item Type

- **Epic Value** — Strategic: answers "why does this capability matter?"
- **Story Value** — Tactical: answers "what specific benefit does shipping this deliver?"
- **Task Value** — Operational: answers "why is this work necessary?" (tasks may reference their parent story's value when they don't carry independent value)

Tasks are the one level where intrinsic value can be inherited — a database migration task
may not have standalone user value, but it should still articulate why it's necessary
("enables the new schema required for feature X").

---

## Definition of Done Framework

DoD must be **specific, measurable, and verifiable**. Vague DoD is worse than no DoD
because it creates false confidence.

### DoD Quality Checklist

A good DoD item answers YES to all of these:
- Can someone unfamiliar with this work verify it? (observable)
- Is there exactly one way to interpret this? (unambiguous)
- Can we check it without subjective judgment? (measurable)
- Does it include the acceptance boundary, not just the happy path? (complete)

### Bad vs Good DoD Examples

| Bad | Good |
|-----|------|
| "User authentication works" | "Users can log in with email/password, receive a JWT, and access protected routes. Invalid credentials return 401. Locked accounts return 403 with a message." |
| "Tests pass" | "Unit tests cover all public methods (>90% line coverage). Integration test validates the full login-to-dashboard flow. All tests pass in CI." |
| "Performance is acceptable" | "P95 response time < 200ms for login endpoint under 100 concurrent users, measured via load test." |

---

## Output Format

The final deliverable is a structured agile project plan. Use this hierarchy:

Read `references/output-templates.md` for the complete templates with all fields.

### Summary Structure

```markdown
# Project Plan: [Project Name]

## Vision Summary
[2-3 sentences from Discovery phase]

## Fundamental Truths
[Numbered list from Archaeologist]

## Epic Overview
| # | Epic | Stories | Intrinsic Value (1-line) | Priority |
|---|------|---------|--------------------------|----------|

## Detailed Breakdown

### Epic 1: [Name]
**Intrinsic Value:** [value statement]
**Definition of Done:** [epic-level DoD]

#### Story 1.1: [Name]
**Intrinsic Value:** [value statement]
**Definition of Done:**
- [ ] [specific, measurable criterion]
- [ ] [specific, measurable criterion]

**Tasks:**
| # | Task | DoD | Estimate |
|---|------|-----|----------|

[...repeat for all stories and epics...]

## Validation Summary
### Risks
### Value Map
### Recommended Iteration Order
### Stakeholder Readiness
```

---

## Practical Guidance

### Scope Calibration

The depth of analysis should match the project size:

| Project Size | Discovery | Elaboration | Validation |
|-------------|-----------|-------------|------------|
| Small (1-2 sprints) | Light: skip Scope Architect, go straight from truths to stories | Single pass per epic | White + Black hats only |
| Medium (1-3 months) | Full 3-agent chain | Full dialectical per epic | All 5 hats |
| Large (3+ months) | Full chain + multi-cycle | Full dialectical + cross-epic dependency analysis | All 5 hats + recommended phasing |

### When to Stop Decomposing

- **Epics** should be deliverable in 1-3 sprints (2-6 weeks of work)
- **Stories** should be completable in a single sprint (1-2 weeks)
- **Tasks** should be completable in 1-3 days
- If a task takes longer than 3 days, it's probably a story

### Common Pitfalls

| Pitfall | How This Skill Prevents It |
|---------|---------------------------|
| Feature factory (building without purpose) | Every item must articulate intrinsic value |
| Scope creep disguised as stories | Challenger agent enforces INVEST + traces back to fundamental truths |
| "Done" means different things to different people | DoD is specific, measurable, verifiable — checked by Challenger |
| Analysis paralysis | Scope calibration table right-sizes the process |
| Dependency spaghetti | Stories must be Independent (INVEST); dependencies are explicitly mapped |

---

## Reference Files

Read the appropriate reference file BEFORE spawning agents:

| File | Contents | When to Read |
|------|----------|-------------|
| `references/discovery-agents.md` | Vision Archaeologist, Scope Architect, Coverage Evaluator prompts | Phase 1: before decomposing the project vision |
| `references/decomposition-agents.md` | Story Advocate, Story Challenger, Story Integrator, Task Decomposer prompts | Phase 2: before elaborating each epic |
| `references/validation-agents.md` | White, Black, Yellow, Red, Blue hat prompts adapted for plan validation | Phase 3: before validating the complete plan |
| `references/output-templates.md` | Complete templates for Epics, Stories, Tasks + Value Framework details | When producing the final output |
