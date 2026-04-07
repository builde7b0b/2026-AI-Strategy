# MVP Build Plan

## Goal

Ship the smallest credible version of the workflow tool in 2–4 days.

## MVP scope

Only include:
- raw note capture
- task structuring
- routing recommendations
- prompt generation
- daily board

Everything else can be staged later.

## Recommended stack

- React
- TypeScript
- Electron or Tauri
- SQLite or lightweight local store

## Phase 1 — shell

Build:
- app shell
- sidebar navigation
- inbox screen
- daily board screen
- local storage

## Phase 2 — task compiler

Add:
- raw note input
- structured task form/output
- task type classification rules
- risk/complexity flags
- plan-first vs execute-now decision

## Phase 3 — routing engine

Add simple heuristics:
- Codex for scoped build tasks
- Claude Code for diagnosis/review
- cheap/local for organization and transforms
- manual for strategy-only items

## Phase 4 — prompt compiler

Generate:
- build prompt
- diagnosis prompt
- review prompt
- user story conversion prompt
- task decomposition prompt

## Phase 5 — board and summary

Add:
- drag/drop or simple status transitions
- complete/block/defer actions
- end-of-day notes
- premium usage burn notes

## Suggested file tree

```text
workflow-tool/
  src/
    components/
    screens/
      InboxScreen.tsx
      BoardScreen.tsx
      TaskDetailScreen.tsx
      MemoryScreen.tsx
      SummaryScreen.tsx
    lib/
      parser.ts
      router.ts
      promptCompiler.ts
      storage.ts
      rules.ts
    types/
      task.ts
      note.ts
      project.ts
    App.tsx
```

## First heuristics to implement

### Route to Codex when
- task uses words like add, build, implement, create
- clear scope is present
- acceptance criteria can be listed

### Route to Claude Code when
- task uses words like investigate, root cause, trace, review, audit, why
- repo/system ambiguity is high
- risk is medium/high

### Route to cheap/local when
- task is summarization
- classification
- rewriting
- task decomposition
- daily planning

## Success criteria

The MVP is good enough when it can:
- accept messy notes
- convert them into useful structured tasks
- recommend the correct lane
- output a solid prompt for the selected lane
- give the user a clean “what next” board

## After MVP

Then add:
- workflow memory
- repo-specific templates
- direct clipboard export
- better analytics
- Ollama support
- API integrations later
