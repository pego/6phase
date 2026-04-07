# Conventions

## Docs Structure

Base: `docs/implementation/`
Pattern: `{designs,plans,test-reports}/YYYY-MM-DD-<slug>-{design,plan,test-report}.md`
Slugs: lowercase, hyphen-separated, short. Create directories as needed.

```
docs/{STATUS.md, architecture/{overview,system-context,decisions}.md, implementation/{designs,plans,test-reports,release-notes}/, runbooks/{local-dev,troubleshooting,deployment}.md}
```

## Git & Branching

Trunk-based, short-lived branches. `main` always deployable. Branches live hours-days.

Branch naming: `<type>/<slug>` (e.g. `feat/checkout-validation`, `fix/billing-race`).
Workflow: branch from `main` → commits → `git rebase main` → squash merge → delete branch.

Branch vs `main`: branch for P1-P2 work, multi-commit, collaborative. `main` for single-commit, docs-only, solo.

PR format: Summary (1-3 lines) + Changes (bullets) + Test evidence + `[D] [P] [T]` links.

## ADRs

`docs/architecture/decisions.md` — single living document, source of truth.

Design Docs (P1) = journey. ADRs = **what we do NOW and why**. Decision changes → update in place.

| Domain | Decision | Why | Since |
|---|---|---|---|
| API | REST + JSON:API | Client diversity, caching | 2026-01-15 |

Trigger: P1 changes technical direction → update ADR row + `Since`.
Detail block (`### [Domain]`) only for changed decisions.

## STATUS.md

Reverse chronological. Statuses: `completed` | `in-progress` | `pending` | `blocked` | `postponed` | `cancelled`
Links: [D]=design [P]=plan [T]=test-report.

```markdown
| Date | Feature | Status | Artifacts |
|---|---|---|---|
| 2026-03-20 | checkout-validation | completed | [D](...) [P](...) [T](...) |
```

Detail block ONLY for deviations/follow-ups. No block = went as planned.
