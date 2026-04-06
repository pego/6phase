# P2: Plan

**Purpose:** Break the approved design into an ordered, testable implementation plan.
**Output:** `plans/YYYY-MM-DD-<slug>-plan.md` (read `shared/conventions.md` for naming and directory structure)

## When to use

More than 3 files, multi-module change, migrations, infrastructure changes, non-trivial refactor.

## Before writing the plan, answer these questions

- What's the hardest part of this? Start there.
- What are the dependencies between steps? What can be parallelized?
- Where will existing interfaces or contracts change?
- What prerequisites need to be in place before development starts?
- What's the test that proves this works end-to-end?
- What's the rollback plan if something goes wrong mid-implementation?

## Writing the plan

Structure as ordered tasks. Each task should specify:
- Which files to create or modify
- What the change does
- How to test it
- Rough size: **S** (< 30 min, few lines), **M** (30 min–2 hrs, moderate changes), **L** (2+ hrs, significant complexity)

Size estimates make P3 scope checks meaningful — "task 2 was planned as S but is actually L" is a clear signal to surface early.

Include a test strategy (unit, integration, E2E, manual) and acceptance criteria.
