---
name: 6phase
description: Mandatory 6-phase development workflow — brainstorm, plan, develop, review & test, document, commit. Use this skill for ANY development task: new features, bug fixes, refactors, infrastructure changes, config changes, or documentation updates. Whenever the user asks to build, fix, add, change, remove, or implement something in code, use this workflow. Even simple tasks go through the fast track (P3 → P6). Triggers on any coding request, implementation task, or software change.
---

# 6phase — Router

## Triage

Classify the task before any code:

| Signal | Track | Path |
|---|---|---|
| Bug fix, docs-only, config, ≤3 files, clear fix | **Fast** | P3 → P6 |
| Obvious approach, 4-10 files, single concern | **Standard** | P1+P2 → P3 → P4 → P5 → P6 |
| Arch decision, unclear reqs, multi-module, major refactor | **Full** | P1 → P2 → P3 → P4 → P5 → P6 |
| Unknown feasibility, new tech, need to explore first | **Spike → Full** | P0 → P1 → ... |

Higher-complexity signal wins. User can override in either direction.

**Multiple tasks in one request:** If the user asks for multiple unrelated things ("fix the login bug and add dark mode"), triage each independently and run them as separate 6phase cycles, sequentially. Mixing unrelated changes in one cycle muddies commits and makes rollback harder. Related changes that form a single coherent feature can stay in one cycle.

**User-provided artifacts:** If the user brings their own design, plan, or partial implementation, don't redo their work. Skip to the appropriate phase:
- User provides a design → skip P1, start at P2
- User provides a plan → skip P1+P2, start at P3
- User provides code to review/test → skip to P4

Emit: `## [6PHASE: SKIP → Px | reason: user provided ...]`

Emit triage result:
```
## [6PHASE: TRIAGE → FAST | reason: ...]
## [6PHASE: TRIAGE → STANDARD | reason: ...]
## [6PHASE: TRIAGE → FULL | reason: ...]
## [6PHASE: TRIAGE → SPIKE | reason: ...]
```

## Phase Tracking

On entering each phase, emit:
```
## [6PHASE: Px-NAME]
```
Example: `## [6PHASE: P3-DEV]`

If you lose track, scan for the last `[6PHASE: Px-...]` marker to recover position.

## Gates

⛔ GATE: Do NOT proceed past P1 until the user approves.
⛔ GATE: Do NOT proceed past P2 until the user approves.
⛔ GATE: Do NOT proceed past P4 until the user approves.

Approval = any affirmative response: "approved", "go ahead", "ok", "looks good", "lgtm", "yep", "ship it", "do it", thumbs up, etc. Use common sense — if the user is clearly saying yes, that's approval.

## Phase Loading

You MUST read the phase file before doing any phase work:

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

For medium-complexity tasks where the approach is clear but needs structure. P1 and P2 merge into a single combined Design & Plan document — one gate instead of two.

Output: `designs/YYYY-MM-DD-<slug>-design-plan.md`
⛔ Single GATE after the combined P1+P2 phase.

After approval, proceed to P3 as normal.

## Fast Track

Fast-track tasks go P3 → P6 only. No design doc, plan, or docs phase.

Before P6, present a brief summary of what changed so the user can glance at it. No formal test report needed, but confirm: **"Tests pass: yes/no. Here's what I changed: ..."**

P6 includes a one-line STATUS.md entry for traceability.

If the task turns out bigger than expected, escalate:
```
## [6PHASE: ESCALATE → STANDARD | reason: ...]
## [6PHASE: ESCALATE → FULL | reason: ...]
```
- Escalate to P1 if the problem is unclear or the approach is uncertain.
- Escalate to P2 if the problem is understood but needs a plan.
- Keep work already done; write design/plan to account for it.

## Scope Check

During P3, if the work is growing beyond what was planned — more files touched, unexpected complexity, cascading changes — surface it early:

```
## [6PHASE: SCOPE CHECK | planned: N files/tasks | actual: M | risk: ...]
```

Present the situation to the user with options:
- Continue with expanded scope (update the plan to reflect reality)
- Cut scope (defer parts to a follow-up task)
- Escalate track (fast → standard, standard → full)

Don't wait until P4 to discover the task was 3x bigger than expected.

## Abort

If the user wants to abandon the current cycle ("stop", "never mind", "drop this"), clean up:
- Unstage any staged changes (`git restore --staged .`)
- Keep design docs and plans as-is — they document the thinking even if the work was abandoned
- Add a STATUS.md entry: `cancelled` with a brief reason
- Emit: `## [6PHASE: ABORT | phase: Px | reason: ...]`

## Looping Back

Phases aren't strictly one-way. When a later phase reveals problems, loop back:

| Situation | Go to | Emit |
|---|---|---|
| Tests fail (minor fix) | P3 | `[6PHASE: P4 → P3 | reason: ...]` |
| Design flaw found in dev or test | P1 | `[6PHASE: P3 → P1 | reason: ...]` |
| Plan wrong but design sound | P2 | `[6PHASE: P3 → P2 | reason: ...]` |

Keep work already done. The updated design/plan accounts for completed work.

## Session Resumption

On a new session for in-progress work, determine current phase:
- Spike code exists, no design doc → P1 (spike is done, move to design)
- Design doc exists, no plan → P2
- Combined design-plan exists, implementation incomplete → P3
- Plan exists, implementation incomplete → P3
- Implementation complete, no test report → P4
- Test report exists, docs not updated → P5
- Everything done, not pushed → P6
- Nothing exists → new task, run triage

## Skill Delegation

At the start of each phase, check the available skills list for any that match the current task's domain. If a relevant skill is installed, use it — it will produce better results than generic instructions for that domain.

This is optional and opportunistic. 6phase works fully standalone. But when a specialized skill is available, lean on it rather than reinventing its expertise.

Examples of when to delegate:
- P1: the task involves UI work and a design skill is available → use it to inform the design
- P3: building a React frontend and a React best-practices skill is available → follow its patterns
- P4: a code-review skill is available → run it as part of the review
- P6: a commit/PR skill is available → use it for commit formatting

When delegating, 6phase still owns the workflow (phase order, gates, tracking markers). The delegated skill owns the domain expertise within that phase.

## Quick Reference

| Phase | Purpose | Key output |
|---|---|---|
| P0 Spike | Explore feasibility with throwaway code | Findings + recommendation |
| P1 Brainstorm | Explore problem, design solution | Design doc |
| P2 Plan | Break design into ordered tasks | Implementation plan |
| P1+P2 Combined | Design & plan in one (standard track) | Combined design-plan doc |
| P3 Dev | Implement the plan | Working code + passing tests |
| P4 Review & Test | Verify it works, user approves | Test report |
| P5 Docs | Update project docs, ADRs, STATUS | Updated documentation |
| P6 Commit | Clean commits, push | Committed & pushed code |
