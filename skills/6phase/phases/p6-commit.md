# P6: Commit

**Purpose:** Create clean commits and push. This is the final phase for both full and fast-track workflows.

## Workflow

`git status` → `git diff` → `git add .` → commit → `git push`

Read `shared/conventions.md` for branching rules.

## Conventional Commits

Format: `<type>(<scope>): <subject>`
Scope is optional. Subject: imperative mood, lowercase, no period, max 72 chars.

Types: `feat`(MINOR) `fix`(PATCH) `docs` `refactor` `test` `chore`(build/CI/deps) `perf` `style`(formatting only) `ci`

Breaking changes: add `!` after type/scope (e.g. `feat!:`) + `BREAKING CHANGE:` footer in body.

Body: what changed, why, modules impacted. Link design/plan/test docs when applicable.

**NEVER mention AI tools, assistants, or co-authors in commits. All commits are authored by the developer.**

## Fast-track STATUS.md entry

If this is a fast-track task (no P5 phase), add a one-line entry to `docs/STATUS.md` before committing:

| Date | Feature | Status | Artifacts |
|---|---|---|---|
| YYYY-MM-DD | slug | completed | — |

No detail block needed for fast-track tasks.

## Done

Docs updated + clean commits pushed + STATUS reflects reality.
