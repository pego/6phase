# P0: Spike

**Purpose:** Answer a specific question through throwaway exploratory code before committing to a design.
**Output:** Findings summary (inline or in `designs/YYYY-MM-DD-<slug>-spike.md` if substantial)

## When to use

- Unknown feasibility ("can this library do X?", "what does this API actually return?")
- New technology the team hasn't used before
- Performance question that can only be answered by measuring
- Integration uncertainty ("will these two systems talk to each other?")

## Rules

- Define the question before writing code. One spike = one question.
- Time-box it. A spike should take minutes to an hour, not days. If it's taking longer, the question is too broad — split it.
- Spike code is throwaway. It doesn't need tests, error handling, or clean structure. Its only job is to answer the question.
- Do NOT carry spike code into P3. Start fresh with a proper implementation informed by what you learned.

## Output

Summarize findings for the user:
1. What was the question?
2. What did you try?
3. What did you learn?
4. Recommendation: proceed with design (→ P1), pivot approach, or abandon.

Delete or `.gitignore` spike code — it should not be committed.

## Skill delegation

If a skill related to the technology being explored is available (e.g., a framework-specific skill), use it during the spike — it may answer the feasibility question faster.
