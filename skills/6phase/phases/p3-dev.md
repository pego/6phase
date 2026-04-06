# P3: Development

**Purpose:** Implement the plan with discipline — passing tests, no surprises.

## Rules

- Follow the plan in order. If you need to diverge, update the plan first.
- Stage changes as you go but do NOT commit during P3. All commits happen in P6 — this keeps the commit history clean and lets the user review everything before it's committed.
- Tests, lint, and build must pass locally before moving to P4.
- If a decision changes the technical direction from the design, update the Design Doc and flag it for ADR update in P5.

## When the project has no test infrastructure

If the project lacks a test runner, linter, or build step:
- For full-track tasks: set up minimal test infrastructure as the first plan step (test framework, a single smoke test). This is part of the deliverable.
- For fast-track tasks: verify manually and note what was checked. Don't build test infrastructure for a 3-line fix.

## Scope check

If the work is growing beyond the plan — more files than expected, cascading changes, unexpected complexity — don't push through silently. Surface it:

```
## [6PHASE: SCOPE CHECK | planned: N files/tasks | actual: M | risk: ...]
```

Present options to the user: continue with expanded scope, cut scope and defer, or escalate track.

## Failure handling

If development hits a blocker (dependency issue, design flaw, unclear requirement):
- Update the plan with what you've learned.
- If the design itself is wrong, escalate back:
```
## [6PHASE: P3 → P1 | reason: ...]
## [6PHASE: P3 → P2 | reason: ...]
```
- Keep work already done; the updated design/plan accounts for it.

## Skill delegation

This is where specialized skills add the most value. Check available skills for any that match the implementation domain — framework best practices (React, Vue, etc.), design systems (shadcn, Tailwind), infrastructure tools, or language-specific patterns. Use them to write better code than generic instructions would produce.

## Output before P4

Provide: implementation summary, test results, manual test instructions (if applicable).
