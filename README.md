# 6phase

A structured, 6-phase development workflow for AI coding agents. Like [12factor.net](https://12factor.net/) for your development process.

No shortcuts. No exceptions.

## The 6 Phases

```
1. BRAINSTORMING       -> Design Document
      ↓ approval gate
2. IMPLEMENTATION PLAN -> Plan Document
      ↓ approval gate
3. DEVELOPMENT         -> Validation Package
      ↓
4. APPROVAL            -> Test Report
      ↓ approval gate
5. DOCUMENTATION       -> Updated docs
      ↓
6. COMMIT & PUSH       -> Clean git history
```

| Phase | Output | Gate |
|-------|--------|------|
| 1. Brainstorming | Design Document | Explicit approval |
| 2. Implementation Plan | Plan Document | Explicit approval |
| 3. Development | Validation Package | Tests pass locally |
| 4. Approval | Test Report | Explicit approval |
| 5. Documentation | Updated STATUS.md & living docs | — |
| 6. Commit & Push | Clean conventional commits | STATUS reflects reality |

## Why

AI coding agents are fast, but speed without structure leads to:

- Skipped designs that cause rework
- Missing documentation that slows down the next session
- Code changes without test evidence
- Commits without context

6phase enforces the discipline that makes AI-assisted development reliable and auditable.

## Install

```bash
npx skills add github:pego/6phase
```

Or install locally:

```bash
npx skills add ./path/to/6phase
```

The skill activates at the start of every prompt session. It determines which phase your current work is in and follows the process from that point.

## How It Works

The skill is structured so that only what's needed is loaded into context at any given time.

- **Session start**: a lightweight router (~70 lines) loads and triages the task
- **Triage result**: tasks are classified as Fast track (P3→P6) or Full track (P1→P6)
- **On-demand loading**: phase instructions load only when that phase is active — prior phases are not in context
- **Phase tracking**: structural markers (`[6PHASE: P3-DEV]`) in the conversation record which phase is current
- **Approval gates**: phases P1, P2, and P4 require explicit user sign-off before the next phase begins

### Skill Structure

```
skills/6phase/
├── SKILL.md              # Router (loaded at session start)
├── phases/
│   ├── p1-brainstorm.md
│   ├── p2-plan.md
│   ├── p3-dev.md
│   ├── p4-approve.md
│   ├── p5-docs.md
│   └── p6-commit.md
└── shared/
    └── conventions.md    # Doc naming, branching, ADRs
```

## Quick Reference

### When to start at which phase

**Full track** — new or non-trivial work that benefits from design and planning:

| Situation | Start at |
|-----------|----------|
| New feature request | Phase 1 |
| Approved design, no plan yet | Phase 2 |
| Approved plan, ready to code | Phase 3 |
| Code complete, needs testing | Phase 4 |

**Fast track** — bug fixes, docs-only, config changes, or anything touching fewer than 3 files. Skips design, plan, and docs phases:

| Situation | Track |
|-----------|-------|
| Bug fix | P3 → P6 |
| Docs-only change | P3 → P6 |
| Config change | P3 → P6 |
| Change touching ≤3 files | P3 → P6 |

### Documentation structure

All artifacts live under `docs/implementation/`:

```
docs/
├── STATUS.md
├── architecture/
├── implementation/
│   ├── designs/      YYYY-MM-DD-<slug>-design.md
│   ├── plans/        YYYY-MM-DD-<slug>-plan.md
│   ├── test-reports/ YYYY-MM-DD-<slug>-test-report.md
│   └── release-notes/
└── runbooks/
```

## License

MIT
