# Seeded Examples

## Example 1 — Messy founder note

### Raw note

> Homepage still feels weak. Hero needs to hit harder. Fix mobile spacing in the cards. Also figure out why signup is failing on iOS. Maybe auth token issue or duplicate create bug. Need demo-ready by tomorrow.

### Structured tasks

#### Task A
- Title: Strengthen homepage hero and card spacing
- Type: UI polish
- Desired outcome: homepage feels sharper and mobile layout looks correct
- Risk: low
- Plan first?: no
- Best route: Codex

#### Task B
- Title: Investigate iOS signup failure
- Type: bug / diagnosis
- Desired outcome: identify root cause and define smallest safe fix
- Risk: high
- Plan first?: yes
- Best route: Claude Code

#### Task C
- Title: Prepare demo readiness checklist
- Type: ops / planning
- Desired outcome: clear next actions for tomorrow demo
- Risk: low
- Plan first?: no
- Best route: cheap/local model

## Example 2 — User story

### Raw story

> As a driver, I want to see whether my payout account is ready before I accept deliveries so I know I can actually get paid.

### Implementation pack
- Summary: surface payout readiness before delivery acceptance
- Acceptance criteria:
  - driver sees payout readiness state clearly
  - blocked state explains next step
  - acceptance flow respects readiness rule if enforced
- Likely route: Codex
- Review route after build: Claude Code

## Example 3 — Review request

### Situation
Codex already shipped a multi-file patch for notifications, but behavior feels inconsistent.

### Best route
Claude Code review prompt:

```text
Review this diff/implementation for correctness, regressions, edge cases, styling drift, state bugs, and unnecessary complexity. Prioritize the top 5 issues only. Suggest minimal fixes, not rewrites.
```

## Example 4 — Cheap lane use

### Raw note

> Turn these 12 random notes into a clean plan for today and mark which items are deep work versus quick wins.

### Best route
cheap/local model

### Why
This is organizational work, not premium implementation work.
