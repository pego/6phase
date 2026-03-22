# Conventions

## Documentation Structure

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

| Domain | Decision | Why | Since |
|---|---|---|---|
| API | REST + JSON:API | Client diversity, caching, tooling | 2026-01-15 |

Update trigger: any P1 Design Doc that changes a technical direction → update ADR row + `Since` date.

Detail block only for changed decisions: `### [Domain]` — what was replaced, link to Design Doc that drove the change.

## STATUS.md Format

Keep compact and token-efficient. Reverse chronological order (most recent first).
Statuses: `completed` | `in-progress` | `pending` | `blocked` | `postponed` | `cancelled`
Artifact links use short labels: [D]=design, [P]=plan, [T]=test-report.

```markdown
# STATUS

| Date | Feature | Status | Artifacts |
|---|---|---|---|
| 2026-03-20 | checkout-validation | completed | [D](...) [P](...) [T](...) |
```

Add a detail block ONLY when there are deviations, follow-ups, or non-obvious context. No detail block = everything went as planned.
