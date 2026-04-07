---
name: 6phase
description: "Mandatory 6-phase development workflow: brainstorm, plan, develop, review and test, document, commit. Use this skill for ANY development task - new features, bug fixes, refactors, infrastructure changes, config changes, or documentation updates. Whenever the user asks to build, fix, add, change, remove, or implement something in code, use this workflow. Even simple tasks go through the fast track (P3 to P6). Triggers on any coding request, implementation task, or software change."
---

# 6phase — Router

## Triage

Classify before coding. Higher-complexity signal wins. User can override.

| Signal | Track | Path |
|---|---|---|
| Bug fix, docs-only, config, ≤3 files | **Fast** | P3 → P6 |
| Clear approach, 4-10 files, single concern | **Standard** | P1+P2 → P3 → P4 → P5 → P6 |
| Arch decision, unclear reqs, multi-module, major refactor | **Full** | P1 → P2 → P3 → P4 → P5 → P6 |
| Unknown feasibility, new tech | **Spike** | P0 → P1 → ... |

**Multi-task:** Unrelated tasks → separate cycles. Related changes forming one feature → one cycle.

**User artifacts:** User provides design → start P2. Plan → start P3. Code → start P4. Emit: `[6PHASE: SKIP → Px | reason: ...]`

Emit: `## [6PHASE: TRIAGE → FAST|STANDARD|FULL|SPIKE | reason: ...]`

## Tracking

On phase entry, emit: `## [6PHASE: Px-NAME]` (e.g. `P3-DEV`). Lost? Scan for last marker.

## Gates

⛔ Do NOT proceed past P1, P2, or P4 without user approval.
Approval = any affirmative: ok, lgtm, go ahead, looks good, yep, ship it, etc.

## Phase Files

Read the phase file before doing any phase work:

| Phase | File |
|---|---|
| P0 Spike | `phases/p0-spike.md` |
| P1 Brainstorm | `phases/p1-brainstorm.md` |
| P2 Plan | `phases/p2-plan.md` |
| P3 Dev | `phases/p3-dev.md` |
| P4 Review & Test | `phases/p4-review.md` |
| P5 Docs | `phases/p5-docs.md` |
| P6 Commit | `phases/p6-commit.md` |

## Standard Track

P1+P2 merged into one document, one gate. Output: `designs/YYYY-MM-DD-<slug>-design-plan.md`

## Fast Track

P3 → P6 only. Before P6, show user a brief summary: "Tests pass: yes/no. Here's what changed: ..." P6 includes a one-line STATUS.md entry.

Escalate if bigger than expected:
`[6PHASE: ESCALATE → STANDARD|FULL | reason: ...]`
Escalate to P1 if unclear, P2 if needs plan. Keep work done.

## Scope Check

During P3, if work exceeds plan — surface early:
`[6PHASE: SCOPE CHECK | planned: N | actual: M | risk: ...]`
Options: expand scope, cut & defer, escalate track.

## Abort

User abandons cycle → unstage changes, keep docs, add STATUS.md `cancelled` entry.
`[6PHASE: ABORT | phase: Px | reason: ...]`

## Looping Back

| Situation | Go to | Emit |
|---|---|---|
| Tests fail (minor) | P3 | `[6PHASE: P4 → P3 | reason: ...]` |
| Design flaw | P1 | `[6PHASE: P3 → P1 | reason: ...]` |
| Plan wrong, design sound | P2 | `[6PHASE: P3 → P2 | reason: ...]` |

Keep completed work. Updated design/plan accounts for it.

## Session Resumption

Determine phase from artifacts: spike exists no design → P1 | design no plan → P2 | plan/design-plan, incomplete impl → P3 | impl complete no test report → P4 | test report, docs outdated → P5 | all done not pushed → P6 | nothing → triage.

## Skill Delegation

At each phase, check available skills for domain matches. Use them — they beat generic instructions. 6phase owns the workflow; delegated skills own domain expertise. Fully optional.

## Quick Reference

| Phase | Purpose | Output |
|---|---|---|
| P0 | Spike: explore feasibility | Findings |
| P1 | Brainstorm: design solution | Design doc |
| P2 | Plan: ordered tasks | Plan |
| P1+P2 | Combined (standard track) | Design-plan |
| P3 | Dev: implement | Code + tests |
| P4 | Review & test | Test report |
| P5 | Docs: update project docs | Documentation |
| P6 | Commit & push | Commits |
