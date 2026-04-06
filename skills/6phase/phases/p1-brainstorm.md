# P1: Brainstorm

**Purpose:** Design a solution before writing code.
**Output:** `designs/YYYY-MM-DD-<slug>-design.md` (see `shared/conventions.md`)

## Answer before writing

- What problem are we solving? (not what feature — what problem)
- What happens if we don't build this?
- Who is affected and how?
- Constraints? (tech, compliance, performance, budget, timeline)
- Current state?
- 2-3 genuinely different approaches? Trade-offs of each?
- Riskiest assumption?
- How will we know it works?
- Rollback plan?
- What's still unclear?

## Writing the design

Structure around your answers. Length matches complexity. If this changes technical direction, update ADR after approval (see `shared/conventions.md`).

## Standard track

If **standard** track: combine P1+P2 into `designs/YYYY-MM-DD-<slug>-design-plan.md`. Design questions above + plan (ordered tasks, files, test strategy). One gate.

Use available design/domain skills to inform approaches and trade-offs.
