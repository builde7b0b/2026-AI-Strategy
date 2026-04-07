# Workflow Operating System

## Stack roles

Use the stack with strict role separation:

- **Cursor** = editor shell and control center
- **Codex** = primary implementation engine
- **Claude Code** = diagnosis, review, architecture planning, and repo surgery
- **Cheap/local model** = summarization, classification, rewrite, decomposition, low-value grunt work

This prevents overlap, duplicated effort, and wasted requests.

## Three-lane model

### Lane 1 — Cheap / repetitive / low-risk
Use a cheaper model or Codex Mini for:

- boilerplate
- copy changes across files
- renames
- test generation
- docs
- small UI tweaks
- formatting-oriented changes

### Lane 2 — Mainline build work
Use Codex for:

- scoped feature implementation
- multi-file edits with clear boundaries
- refactors with acceptance criteria
- prompt-driven code generation
- patching known problems

### Lane 3 — High-risk or ambiguous work
Use Claude Code for:

- diagnosis-first tasks
- root cause analysis
- strange regressions
- repo audits
- architectural comparisons
- review before merge
- shell-heavy investigation

## The core loop

1. **Decompose** the work from raw notes into clear tasks
2. **Route** each task to the correct model/tool
3. **Prompt** with scope, constraints, and acceptance criteria
4. **Review** output with a second-pass model only when needed
5. **Patch** only the approved fixes
6. **Log** what burned premium usage and why

## Routing rules

### Send to Codex when

- the implementation target is known
- files are identifiable
- the work is mainly build/edit/refactor
- the task has clear acceptance criteria
- you want direct patches

### Send to Claude Code when

- the diagnosis is unclear
- the bug spans multiple systems
- terminal investigation matters
- you need to review another model’s output
- you want a plan before any patching

### Send to cheap/local model when

- the task is summarization
- the task is classification
- the task is rewriting notes into tickets
- the task is extracting acceptance criteria
- the task is organizing daily work

## Anti-limit rules

- Never ask both Codex and Claude to solve the same broad task from scratch
- Never use expensive models for repo discovery more than once per repo/session pattern
- Never mix diagnosis, implementation, review, and documentation in one giant request
- Never send vague prompts when the task can be scoped first
- Always separate **plan first** from **patch now** when uncertainty is high
- Always prefer the cheapest reliable model for the task

## Prompt shape by task type

### Build prompt
- Goal
- Scope
- Constraints
- Acceptance criteria
- Output requested
- Verification commands

### Diagnosis prompt
- Symptom
- Expected behavior
- Repro steps
- Suspected area
- Ask for root cause first
- Ask for the smallest safe fix plan

### Review prompt
- Review this diff or implementation
- Find regressions and unnecessary complexity
- Prioritize top issues only
- Recommend minimal fixes, not rewrites

## Daily execution philosophy

Build the day like a portfolio of work:

- **Deep work** = high-value tasks that deserve premium model usage
- **Quick wins** = cheap tasks for momentum and cleanup
- **Review tasks** = verification and quality passes
- **Low-energy tasks** = admin, docs, transforms, and planning

The operating system should answer two questions at all times:

1. **What should I do next?**
2. **Which tool should handle it?**

## Founder efficiency rules

- Codex builds
- Claude diagnoses and reviews
- Always include acceptance criteria on build tasks
- Always track which tasks consumed premium usage
- Always reuse workflow memory instead of re-explaining the repo
- Always turn messy notes into scoped requests before using expensive models
- Always default to a smaller/cheaper lane unless the task proves it needs more
