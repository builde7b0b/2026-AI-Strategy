# Product Spec — Workflow Tool

## Purpose

Build a local-first internal execution tool that turns messy notes, user stories, and daily founder inputs into structured work for AI-assisted software development.

The tool exists to reduce prompt waste, improve task shaping, and help route work correctly between Codex, Claude Code, and cheaper/local model lanes.

## Core problem

Most wasted AI usage does not come from weak tools. It comes from:

- vague requests
- mixed task types in one prompt
- repeated repo explanation
- using expensive models for low-value work
- poor separation between diagnosis, implementation, and review

This product solves that by acting as a task compiler and workflow router.

## Target user

Initial user:

- solo founder
- software engineer
- technical operator
- works from messy notes
- uses Cursor as primary shell
- uses Codex as builder
- uses Claude Code as reviewer/debugger/planner
- wants tighter execution and lower waste

## Product thesis

This is not a generic todo app.
It is a personal AI execution operating system.

It should answer two questions:

1. What should I do next?
2. Which tool should handle it?

## Core sections

### 1. Inbox
Fast raw note capture for:
- ideas
- bug notes
- user stories
- pasted logs
- screenshots notes
- ops/admin items
- outreach/content tasks

### 2. Structurer
Transforms raw input into:
- title
- task type
- desired outcome
- risk
- scope
- dependencies
- whether to plan first

### 3. Model router
Routes work to:
- Codex Mini / cheap lane
- Codex
- Claude Code
- manual only
- defer

### 4. Prompt compiler
Generates efficient prompts with:
- goal
- scope
- constraints
- acceptance criteria
- output requested
- verification steps

### 5. Daily board
Tracks:
- raw intake
- ready to scope
- ready to prompt
- in progress
- waiting on review
- blocked
- done
- defer later

### 6. Workflow memory
Stores repo-level instructions such as:
- build/test commands
- safe edit zones
- high-risk files
- platform gotchas
- prompt preferences
- release/review rituals

### 7. End-of-day summary
Shows:
- completed tasks
- blocked tasks
- premium usage burn patterns
- carry-forward work
- prompts that worked well

## Product logic

### Routing philosophy
- Codex builds
- Claude diagnoses and reviews
- cheap/local models organize and transform
- manual decisions stay manual when founder judgment is required

### Efficiency rules
- never use premium model power for low-value grunt work
- never send vague prompts when the task can be scoped first
- always separate diagnosis from implementation
- always include acceptance criteria for build tasks
- always track what kind of task burned expensive usage
- always reuse workflow memory instead of re-explaining context
- always recommend the cheapest model that can reliably do the job

## MVP requirements

Must have:
- local persistence
- inbox capture
- task structuring
- model routing
- prompt generation
- daily board
- workflow memory
- end-of-day summary

## UX direction

- dark-mode first
- minimal and premium
- fast capture
- card-based clarity
- color-coded routing
- low-clutter execution UI

Suggested routing colors:
- blue = Codex
- purple = Claude Code
- green = cheap/local
- amber = manual/review-needed
- red = blocked/high risk

## Stack recommendation

- Electron or Tauri
- React
- TypeScript
- SQLite
- local JSON export/import for portability

## Non-goals for MVP

Do not build yet:
- direct model API execution inside the app
- complex collaboration/team features
- bloated project management features
- full analytics dashboard
- plugin marketplace behavior

## Outcome

The product should make it easier to convert raw founder chaos into clean execution packets that are ready for the right AI tool.