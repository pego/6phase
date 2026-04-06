# P2: Plan

**Purpose:** Break approved design into ordered, testable tasks.
**Output:** `plans/YYYY-MM-DD-<slug>-plan.md` (see `shared/conventions.md`)

## Answer before writing

- Hardest part? Start there.
- Dependencies between steps? What can parallelize?
- Where do interfaces/contracts change?
- Prerequisites before dev starts?
- End-to-end acceptance test?
- Rollback plan mid-implementation?

## Writing the plan

Ordered tasks, each with:
- Files to create/modify
- What changes
- How to test
- Size: **S** (few lines) / **M** (moderate) / **L** (significant complexity)

Sizes feed P3 scope checks — "planned S, actually L" is a signal.

Include test strategy (unit/integration/E2E/manual) and acceptance criteria.
