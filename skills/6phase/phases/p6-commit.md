# P6: Commit

**Purpose:** Clean commits and push. Final phase for all tracks.

## Workflow

`git status` → `git diff` → `git add .` → commit → `git push`
See `shared/conventions.md` for branching rules.

## Conventional Commits

Format: `<type>(<scope>): <subject>` — imperative, lowercase, no period, ≤72 chars. Scope optional.

Types: `feat`(MINOR) `fix`(PATCH) `docs` `refactor` `test` `chore` `perf` `style` `ci`

Breaking: `feat!:` + `BREAKING CHANGE:` footer.
Body: what, why, modules impacted. Link design/plan/test docs.

**NEVER mention AI tools, assistants, or co-authors in commits. All commits are authored by the developer.**

## Fast-track STATUS.md

No P5 → add one-line entry to `docs/STATUS.md` before committing:
`| YYYY-MM-DD | slug | completed | — |`

Use available commit/PR skills for project-specific conventions.

## Done

Docs updated + commits pushed + STATUS reflects reality.
