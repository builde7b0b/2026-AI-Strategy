# Prompt Routing Templates

## 1. Scoped build request (Codex)

```text
Goal: [one sentence]
Scope: [files or folders]
Constraints: [what must not change]
Acceptance criteria:
- [criterion]
- [criterion]
Output: [patch now / plan first / include tests]
Verify: [commands or checks]
```

Use when the work is implementation-heavy and you already know what should be built.

---

## 2. Diagnosis-first request (Claude Code)

```text
Symptom: [exact issue]
Expected: [desired behavior]
Repro: [steps]
Suspected area: [files/modules]
Ask: diagnose root cause first, then propose the smallest safe fix.
Do not patch yet.
```

Use when the problem is ambiguous or likely spans multiple systems.

---

## 3. Review request (Claude Code)

```text
Review this diff/implementation for correctness, regressions, edge cases, styling drift, state bugs, and unnecessary complexity. Prioritize the top 5 issues only. Suggest minimal fixes, not rewrites.
```

Use after Codex has already built a first pass.

---

## 4. Task decomposition request (cheap/local model)

```text
Turn these raw notes into a structured execution list.
For each item, provide:
- title
- task type
- desired outcome
- risk
- whether this needs plan-first or can be executed directly
- best route: Codex Mini, Codex, Claude Code, or manual only

Raw notes:
[paste notes]
```

Use this before spending premium requests on vague work.

---

## 5. User story to implementation pack

```text
Convert this user story into an implementation pack.
Return:
- summary
- assumptions
- acceptance criteria
- subtasks
- likely files affected
- risks
- best model/tool route
- final build prompt

User story:
[paste story]
```

---

## 6. UI bug request

```text
Fix this UI issue.
Goal: [one sentence]
Scope: [component(s)/screen(s)]
Constraints:
- visual/styling changes only unless strictly necessary
- do not change unrelated logic
Acceptance criteria:
- [criterion]
- [criterion]
Output: patch now and summarize changed files
Verify: explain how to validate manually
```

---

## 7. Batch cleanup request

```text
Apply this small repetitive change across the codebase.
Change required: [description]
Scope: [folders/files]
Constraints: keep behavior unchanged
Output: patch all applicable files and summarize patterns updated
```

Use the cheapest reliable model lane possible.

---

## Routing reminder

- **Codex builds**
- **Claude diagnoses and reviews**
- **Cheap/local model organizes and transforms**
- **Manual only handles founder judgment and strategic decisions**
