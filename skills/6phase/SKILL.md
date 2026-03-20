---
name: 6phase
description: Mandatory 6-phase development workflow — brainstorm, plan, develop, test, document, commit. Enforces structured, stack-agnostic delivery with approval gates.
---

# 6phase

Mandatory 6-phase dev workflow. No shortcuts. No exceptions.

P1:BRAINSTORM [gate] → P2:PLAN [gate] → P3:DEV → P4:APPROVE [gate] → P5:DOCS → P6:COMMIT

## Entry Point

Determine phase at session start before any code:
- New feature → P1
- Design approved, no plan → P2
- Plan approved / bug fix / <3 files → P3
- Code complete → P4

## Conventions

Base path: `docs/implementation/`
File pattern: `{designs,plans,test-reports}/YYYY-MM-DD-<slug>-{design,plan,test-report}.md`
Slugs: lowercase, hyphen-separated, short+specific.

```
docs/{STATUS.md, architecture/{overview,system-context,decisions}.md, implementation/{designs,plans,test-reports,release-notes}/, runbooks/{local-dev,troubleshooting,deployment}.md}
```

## Git & Branching

Trunk-based dev with short-lived feature branches. `main` is always deployable. Branches live hours to days, not weeks.

Branch naming: `<type>/<slug>` — types mirror conventional commits (e.g. `feat/checkout-validation`, `fix/billing-race`).

Workflow: branch from `main` → atomic commits → `git rebase main` → squash merge → delete branch.

When to branch vs. `main` directly:
- Branch: P1-P2 work, multi-commit, collaborative
- `main`: single-commit fixes, docs-only, solo simple changes

PR format (when used): Summary (1-3 lines) + Changes (bullets) + Test evidence + Artifact links `[D] [P] [T]`.

## Architecture Decision Records

`docs/architecture/decisions.md` — **single living document**, current source of truth for technical decisions.

Design Docs (P1) = the journey (options, trade-offs, context). ADRs = **what we do NOW and why**. Decision changes → update ADR in place; the Design Doc preserves history.

Format — table with one row per decision domain:

```markdown
| Domain | Decision | Why | Since |
|---|---|---|---|
| API | REST + JSON:API | Client diversity, caching, tooling | 2026-01-15 |
| DB | PostgreSQL | Relational + JSONB flexibility | 2026-01-15 |
| Queue | SQS | Managed, no ops overhead | 2026-02-10 |
```

Update trigger: any P1 Design Doc that changes a technical direction → update ADR row + `Since` date.

Detail block only for changed decisions: `### Queue` — what was replaced, link to Design Doc that drove the change.

## P1: Brainstorm

When: new feature, arch decision, unclear reqs, multi-subsystem, major refactor.
Output: `designs/YYYY-MM-DD-<slug>-design.md`
Sections: 1)Executive Summary 2)Problem Statement 3)Scope(in/out) 4)Constraints(tech/compliance/perf/budget) 5)Current State 6)Options(2-3,pros/cons) 7)Proposed Solution(arch,components,interfaces,data flow) 8)Decision Rationale 9)Risks→Mitigations 10)Testing & Observability 11)Rollback 12)Open Questions
**GATE: Explicit user approval.**

## P2: Plan

When: >3 files OR multi-module OR migrations/infra/non-trivial refactor.
Output: `plans/YYYY-MM-DD-<slug>-plan.md`
Sections: 1)Overview 2)Prerequisites 3)Impacted Areas 4)API/Contracts(if any) 5)Schema Changes(if any) 6)Step-by-Step Tasks(ordered;files,action,tests each) 7)Test Strategy(unit/integ/E2E/perf/manual) 8)Acceptance Criteria 9)Rollback Plan 10)Release Plan
**GATE: Explicit user approval.**

## P3: Dev

Rules: Follow plan in order (diverge→update plan first). Atomic commits. Tests+lint+build pass locally. Design-changing decisions→update Design Doc + ADR if it changes a technical direction.
Output before P4: implementation summary, test results, manual test instructions.

## P4: Approve

Confirm implementation matches expectations in real usage.
Output: `test-reports/YYYY-MM-DD-<slug>-test-report.md`
Sections: 1)Automated Tests(unit/integ/E2E/static→pass/fail) 2)Manual Test Cases(steps,expected,actual) 3)Verdict(approved/issues/changes needed)
**GATE: Explicit user approval.**

## P5: Docs

1. Update `docs/STATUS.md` (see format below)
2. Update `docs/architecture/decisions.md` if any technical direction changed (see ADR format above)
3. Update `docs/architecture/*` or `docs/runbooks/*` as needed
4. Mark Design/Plan as Complete, note deviations

### STATUS.md Format

Keep compact and token-efficient. Reverse chronological order (most recent first).
Statuses: `completed` | `in-progress` | `pending` | `blocked` | `postponed` | `cancelled`
Artifact links use short labels: [D]=design, [P]=plan, [T]=test-report.

```markdown
# STATUS

| Date | Feature | Status | Artifacts |
|---|---|---|---|
| 2026-03-20 | checkout-validation | completed | [D](implementation/designs/...) [P](implementation/plans/...) [T](implementation/test-reports/...) |
| 2026-03-18 | billing-webhooks | blocked | [D](implementation/designs/...) |
| 2026-03-15 | rbac-admin | postponed | — |
```

Add a detail block ONLY when there are deviations, follow-ups, or non-obvious context:

```markdown
### checkout-validation
Deviations: dropped address autocomplete (API cost). Follow-up: revisit Q3.
```

No detail block = everything went as planned.

## P6: Commit

`git status`→`git diff`→`git add .`→commit→`git push`

### Conventional Commits

Format: `<type>(<scope>): <subject>`
Scope is optional. Subject: imperative mood, lowercase, no period, max 72 chars.

Types: `feat`(MINOR) `fix`(PATCH) `docs` `refactor` `test` `chore`(build/CI/deps) `perf` `style`(formatting only) `ci`

Breaking changes: add `!` after type/scope (e.g. `feat!:`) + `BREAKING CHANGE:` footer in body.

Body: what changed, why, modules impacted. Link design/plan/test docs when applicable.

**NEVER mention AI tools, assistants, or co-authors in commits. All commits are authored by the developer.**

**Done** = docs updated + clean commits pushed + STATUS reflects reality.
