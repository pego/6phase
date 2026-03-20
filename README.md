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

## Quick Reference

### When to start at which phase

| Situation | Start at |
|-----------|----------|
| New feature request | Phase 1 |
| Approved design, no plan yet | Phase 2 |
| Approved plan, ready to code | Phase 3 |
| Code complete, needs testing | Phase 4 |
| Bug fix or small change (<3 files) | Phase 3 |

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
