# P4: Review & Test

**Purpose:** Verify the implementation works as expected through testing and user review.
**Output:** `test-reports/YYYY-MM-DD-<slug>-test-report.md` (read `shared/conventions.md` for naming and directory structure)

## Test report contents

1. **Automated tests** — unit, integration, E2E, static analysis. State pass/fail for each.
2. **Manual test cases** — steps to reproduce, expected result, actual result.
3. **Verdict** — approved, issues found, or changes needed.

## What to verify

- Does the implementation match the design intent?
- Do edge cases behave correctly?
- Is the user experience acceptable?
- Are there performance concerns?

## Failure handling

If testing reveals issues:
- Minor fixes (typos, off-by-one, small logic errors): fix in P3, re-run tests, return to P4.
- Design-level issues (wrong approach, missing requirements): escalate back to P1 or P2 as appropriate.

Emit when looping back:
```
## [6PHASE: P4 → P3 | reason: ...]
## [6PHASE: P4 → P1 | reason: ...]
```

## Skill delegation

If a code-review or testing skill is available, use it as part of this phase. It can catch issues that manual review misses — security patterns, accessibility, performance anti-patterns, framework-specific pitfalls.
