```
 █████╗  ██████╗  ██╗  ██╗  █████╗  ███████╗ ███████╗
██╔═══╝  ██╔══██╗ ██║  ██║ ██╔══██╗ ██╔════╝ ██╔════╝
██████╗  ██████╔╝ ███████║ ███████║ ███████╗ █████╗
██╔══██╗ ██╔═══╝  ██╔══██║ ██╔══██║ ╚════██║ ██╔══╝
╚█████╔╝ ██║      ██║  ██║ ██║  ██║ ███████║ ███████╗
 ╚════╝  ╚═╝      ╚═╝  ╚═╝ ╚═╝  ╚═╝ ╚══════╝ ╚══════╝
```

A structured, 6-phase development workflow for AI coding agents. Like [12factor.net](https://12factor.net/) for your development process.

No shortcuts. No exceptions.

```
  BRAINSTORM ──gate──> PLAN ──gate──> DEVELOP ──> APPROVE ──gate──> DOCUMENT ──> COMMIT
      P1                P2              P3           P4                P5          P6
```

---

## Quickstart

**Install** the skill and start working. That's it.

```bash
npx skills add github:pego/6phase
```

The skill activates automatically at the start of every session. It reads your project state, classifies your task, and guides you through the right phases.

**Small task?** (bug fix, config change, docs update) — the agent goes straight to coding and committing. No ceremony.

**Big task?** (new feature, refactor, architecture decision) — the agent walks you through design, planning, development, testing, documentation, and commit. You approve at three gates before it moves forward.

You stay in control. The agent does the process work.

---

## The Problem

AI coding agents are fast, but speed without structure leads to:

- Skipped designs that cause rework
- Missing documentation that slows the next session
- Code changes without test evidence
- Commits without context
- Context windows filled with irrelevant instructions

6phase enforces the discipline that makes AI-assisted development reliable and auditable — while staying lean on tokens.

---

## How It Works

### Context-Aware Architecture

Most workflow skills dump their entire rulebook into context at session start. 6phase doesn't. It uses a **modular router** pattern:

1. A lightweight router (~70 lines) loads at session start
2. The router **triages** your task as Fast or Full track
3. Phase-specific instructions load **on demand** — only the current phase is in context
4. Prior phase instructions are never competing for the agent's attention

This means ~65% fewer tokens at session start compared to a monolithic skill, and the agent only ever sees instructions relevant to what it's doing right now.

### Two Tracks

| Signal | Track | Path |
|--------|-------|------|
| Bug fix, docs-only, config, ≤3 files, clear fix | **Fast** | P3 → P6 |
| New feature, arch decision, unclear reqs, multi-module, refactor | **Full** | P1 → P2 → P3 → P4 → P5 → P6 |

Any Full signal overrides all Fast signals. You can override in either direction.

### Phase Tracking

The agent emits structural markers as it moves through phases:

```
## [6PHASE: TRIAGE → FULL | reason: new checkout flow spanning 3 modules]
## [6PHASE: P1-BRAINSTORM]
## [6PHASE: P3-DEV]
```

These markers serve as anchoring points. If the agent drifts during a long conversation, it scans for the last marker to recover its position.

### Approval Gates

Three hard gates require your explicit sign-off before the agent proceeds:

| After Phase | What You're Approving |
|-------------|----------------------|
| P1: Brainstorm | The design direction and approach |
| P2: Plan | The implementation plan and task breakdown |
| P4: Approve | The implementation works as expected |

The agent will not move past these gates without hearing "approved" or "go ahead" from you.

### Escalation

If the agent starts on the fast track and discovers the task is bigger than expected, it escalates:

```
## [6PHASE: ESCALATE → FULL | reason: touching 5 modules, need a design]
```

Work already done is kept. The design or plan is written to account for it.

---

## The 6 Phases

### P1: Brainstorm

**When:** New feature, architecture decision, unclear requirements, multi-subsystem change, major refactor.

**Output:** `docs/implementation/designs/YYYY-MM-DD-<slug>-design.md`

Instead of filling in a template, the agent answers probing questions that force genuine thinking:

- What problem are we actually solving?
- What happens if we don't build this?
- What are 2-3 genuinely different approaches?
- What's the riskiest assumption?
- What breaks if we're wrong?

The document's length matches the problem's complexity — 10 lines for something simple, 200 for something complex. No mandatory section count.

**Gate: explicit user approval.**

### P2: Plan

**When:** More than 3 files, multi-module change, migrations, infrastructure, non-trivial refactor.

**Output:** `docs/implementation/plans/YYYY-MM-DD-<slug>-plan.md`

The agent works through:

- What's the hardest part? Start there.
- What are the dependencies between steps?
- Where will existing interfaces change?
- What's the end-to-end test that proves this works?

Structured as ordered tasks, each specifying files, changes, and how to test.

**Gate: explicit user approval.**

### P3: Development

**When:** Plan approved (full track) or task triaged as fast track.

Rules:
- Follow the plan in order. Diverge? Update the plan first.
- Atomic commits — each one builds and passes tests.
- Tests, lint, and build must pass locally.

### P4: Approval

**When:** Code complete (full track only).

**Output:** `docs/implementation/test-reports/YYYY-MM-DD-<slug>-test-report.md`

The agent produces a test report with automated test results, manual test cases, and a verdict.

On fast track, this is replaced by a lightweight "tests pass: yes/no" confirmation — no formal report.

**Gate: explicit user approval.**

### P5: Documentation

**When:** After approval (full track only).

The agent updates:
1. `docs/STATUS.md` — project status tracker
2. `docs/architecture/decisions.md` — if technical direction changed
3. Runbooks and architecture docs as needed
4. Marks design and plan as complete, notes deviations

### P6: Commit

**When:** Final phase for both tracks.

Clean conventional commits, push, and confirm STATUS.md reflects reality.

On fast track, P6 also adds a one-line STATUS.md entry for traceability.

---

## Session Resumption

Starting a new session on in-progress work? The router reads your project state and picks up where you left off:

| Project State | Enters At |
|---------------|-----------|
| Design doc exists, no plan | P2 |
| Plan exists, implementation incomplete | P3 |
| Implementation complete, no test report | P4 |
| Test report exists, docs not updated | P5 |
| Everything done, not pushed | P6 |
| Nothing exists | New task — run triage |

---

## Conventions

6phase includes shared conventions loaded on demand by phase files. These cover:

**Documentation** — all artifacts live under `docs/implementation/`:

```
docs/
├── STATUS.md                          # Project status tracker
├── architecture/
│   ├── overview.md
│   ├── system-context.md
│   └── decisions.md                   # Living ADR document
├── implementation/
│   ├── designs/                       # YYYY-MM-DD-<slug>-design.md
│   ├── plans/                         # YYYY-MM-DD-<slug>-plan.md
│   ├── test-reports/                  # YYYY-MM-DD-<slug>-test-report.md
│   └── release-notes/
└── runbooks/
    ├── local-dev.md
    ├── troubleshooting.md
    └── deployment.md
```

**Git** — trunk-based development with short-lived feature branches. Branch naming follows `<type>/<slug>` (e.g. `feat/checkout-validation`, `fix/billing-race`). Conventional commits with imperative mood, max 72 chars.

**Architecture Decision Records** — a single living document (`docs/architecture/decisions.md`) tracking current technical decisions. Design docs preserve the journey; ADRs show the current state.

**STATUS.md** — compact, token-efficient project tracker. Reverse chronological. Links to artifacts with short labels: `[D]` design, `[P]` plan, `[T]` test report.

---

## Skill Structure

```
skills/6phase/
├── SKILL.md              # Router — triage, gates, phase loading (~70 lines)
├── phases/
│   ├── p1-brainstorm.md  # Design thinking via probing questions
│   ├── p2-plan.md        # Implementation planning via probing questions
│   ├── p3-dev.md         # Development rules
│   ├── p4-approve.md     # Test report and approval
│   ├── p5-docs.md        # Documentation updates
│   └── p6-commit.md      # Git workflow and conventional commits
└── shared/
    └── conventions.md    # Doc naming, branching, ADRs, STATUS.md format
```

Only `SKILL.md` loads at session start. Phase files and conventions load on demand.

---

## Install

### From GitHub

```bash
npx skills add github:pego/6phase
```

### From local directory

```bash
npx skills add ./path/to/6phase
```

### Verify

Start a new session and give the agent a task. You should see a triage marker:

```
## [6PHASE: TRIAGE → FAST | reason: single-file bug fix]
```

or

```
## [6PHASE: TRIAGE → FULL | reason: new feature spanning multiple modules]
```

---

## Contributing

Contributions are welcome. Please open an issue first to discuss what you'd like to change.

## License

MIT
