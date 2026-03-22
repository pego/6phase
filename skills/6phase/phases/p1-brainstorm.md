# P1: Brainstorm

**Purpose:** Explore the problem space and design a solution before writing code.
**Output:** `designs/YYYY-MM-DD-<slug>-design.md` (read `shared/conventions.md` for naming and directory structure)

## When to use

New feature, architecture decision, unclear requirements, multi-subsystem change, major refactor.

## Before writing the design, answer these questions

- What problem are we actually solving? (not what feature — what problem)
- What happens if we don't build this?
- Who is affected and how?
- What constraints exist? (tech, compliance, performance, budget, timeline)
- What does the current state look like?
- What are 2-3 genuinely different approaches? (not "do it" vs "don't do it")
- For each approach: what are the real trade-offs? What breaks? What gets easier?
- What's the riskiest assumption in the proposed solution?
- How will we know it works? (testing, observability)
- How do we roll back if it doesn't?
- What's still unclear?

## Writing the design

Structure the document around your answers. Let the complexity of the problem drive the length — a simple feature might need 10 lines, a complex one 200. No mandatory section count.

If this changes a technical direction, update the ADR after approval (read `shared/conventions.md` for ADR format).
