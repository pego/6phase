# P4: Review & Test

**Purpose:** Verify implementation through testing and user review.
**Output:** `test-reports/YYYY-MM-DD-<slug>-test-report.md` (see `shared/conventions.md`)

## Test report

1. **Automated** — unit, integration, E2E, static analysis. Pass/fail each.
2. **Manual** — steps, expected result, actual result.
3. **Verdict** — approved, issues found, or changes needed.

## Verify

- Matches design intent? Edge cases? UX acceptable? Performance?

## Failures

- Minor (typo, off-by-one): → P3, fix, return. `[6PHASE: P4 → P3 | reason: ...]`
- Design-level: → P1 or P2. `[6PHASE: P4 → P1 | reason: ...]`

Use available code-review/testing skills for deeper analysis.
