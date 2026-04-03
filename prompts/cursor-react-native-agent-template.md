# Cursor Starter Prompts — React Native Agent Template + 3 Hero Demos

Copy/paste these prompts into **Cursor Chat** in order.

> Rule for Cursor (paste once before you start):
>
> **When you generate code:**
> - Always include full file contents (not snippets) for every file you touch.
> - If you reference a file, create it.
> - Prefer simple implementations that run immediately.
> - No TODOs unless absolutely required.
> - After code, include exact commands to run and how to verify in the simulator.

---

## Prompt 0 — Repo bootstrap (React Native + Expo)

```text
You are my senior React Native engineer. We are building an Expo React Native app in TypeScript.

Goal: create a monorepo-style structure with a single Expo app plus a shared /packages folder for reusable agent modules.

Do this now:
1) Initialize Expo app (TypeScript).
2) Create folders:
   - apps/mobile (Expo app)
   - packages/agent-core
   - packages/connectors
   - packages/memory
   - packages/logging
   - packages/permissions
   - packages/ui
3) Set up path aliases so the mobile app can import from packages/* cleanly.
4) Add ESLint + Prettier + basic lint scripts.
5) Create a minimal home screen that proves imports work (render a component from packages/ui).

Return:
- exact file tree
- exact commands to run
- all code for each created file
No explanations. If anything is ambiguous, pick a reasonable default and proceed.
```

---

## Prompt 1 — Agent Core: tools + task runner

```text
Build the shared agent core in /packages/agent-core.

Requirements:
- TypeScript
- No external agent framework required; build simple primitives.
- Provide:
  1) Tool registry: define tools with name, description, input schema (zod), and async handler.
  2) Agent runner: accepts a "plan" array of tool calls and executes them with retries + timeouts.
  3) Event log hooks: emits events for TOOL_START/TOOL_SUCCESS/TOOL_ERROR/AGENT_DONE.
  4) Safe defaults: max steps, max retries, timeout per tool.

Create:
- packages/agent-core/src/index.ts exporting everything
- packages/agent-core/src/types.ts
- packages/agent-core/src/toolRegistry.ts
- packages/agent-core/src/agentRunner.ts

Also create a basic unit test file showing tool execution works.

Return the full code for all files.
```

---

## Prompt 2 — Memory module (local-first)

```text
Implement /packages/memory as a local-first memory store for React Native.

Constraints:
- Must work in Expo.
- Use AsyncStorage as the persistence layer.
- Implement:
  - shortTerm: in-memory map with TTL
  - longTerm: AsyncStorage-backed key/value store
  - "facts": append-only list of typed facts {id, type, content, createdAt}
  - simple search: keyword match over facts
- Include a lightweight "encryption" placeholder layer (interface + no-op implementation) so we can swap later.

Create:
- packages/memory/src/index.ts
- packages/memory/src/storage.ts
- packages/memory/src/shortTerm.ts
- packages/memory/src/longTerm.ts
- packages/memory/src/facts.ts
- packages/memory/src/search.ts
- packages/memory/src/crypto.ts

Return complete code.
```

---

## Prompt 3 — Logging module (structured)

```text
Implement /packages/logging for structured logs.

Requirements:
- Log entries: {id, ts, level, scope, message, data?}
- Support: info/warn/error/debug
- Persist to AsyncStorage (keep last N=2000 logs)
- Provide "exportLogs()" that returns JSON string
- Provide "attachListener" for real-time UI updates

Create:
- packages/logging/src/index.ts
- packages/logging/src/logger.ts
- packages/logging/src/storage.ts

Return full code.
```

---

## Prompt 4 — Permissions module (approve risky actions)

```text
Implement /packages/permissions.

Goal: a permission gate for tools.

Requirements:
- Permission levels: READ_ONLY, NORMAL, SENSITIVE
- Each tool has a required level.
- Provide a PermissionManager that:
  - holds current mode (default READ_ONLY)
  - checks if tool call is allowed
  - if not allowed, returns a structured "needsApproval" object we can render in UI
- Include an allowlist for specific tools even in READ_ONLY.

Create:
- packages/permissions/src/index.ts
- packages/permissions/src/permissions.ts
- packages/permissions/src/permissionManager.ts

Return full code.
```

---

## Prompt 5 — Connectors module (stubs)

```text
Implement /packages/connectors as thin wrappers to external systems.
For today, create 3 connectors as working stubs (no real API keys required):

1) EmailConnector:
   - listThreads()
   - readThread(threadId)
   - draftReply(threadId, body)
   - sendReply(threadId, body)  // for now: fake send, logs action

2) CalendarConnector:
   - listToday()
   - createEvent({title, start, end, location, notes})

3) HttpConnector:
   - get(url)
   - post(url, json)

Each connector must:
- use the logging package
- return mocked sample data if not configured

Create:
- packages/connectors/src/index.ts
- packages/connectors/src/email.ts
- packages/connectors/src/calendar.ts
- packages/connectors/src/http.ts
- packages/connectors/src/config.ts

Return full code.
```

---

# Hero Demo #1 — Inbox Voice Agent

## Prompt 6 — Mobile UI: Inbox agent screen

```text
In apps/mobile, build a new screen called InboxAgentScreen.

UI requirements:
- A list of email threads (from EmailConnector.listThreads)
- Tap thread → show messages
- A big button: "Generate Reply" which calls a local function that:
  - summarizes the thread
  - drafts a reply
  - logs the plan
- Another button: "Send Reply" (calls connector sendReply)
- Add a "Voice" button that uses Expo Speech-to-Text (or placeholder) to capture a spoken instruction like:
  "Reply politely asking for availability next week"
  If speech-to-text is not available, implement a modal text input as fallback.

Architecture requirements:
- Use shared agent-core to execute a plan of tool calls.
- Tools for this demo:
  - readThread
  - summarizeThread
  - draftReply
  - sendReply

Create any new files needed and wire into navigation from Home.

Return exact code changes + files.
```

## Prompt 7 — Tools for inbox agent

```text
Create the actual tools in packages/agent-core OR a new package packages/agent-demos/inbox.

Tools:
- readThreadTool: uses EmailConnector.readThread
- summarizeThreadTool: naive summarizer (no external LLM yet) -> bullet summary
- draftReplyTool: template-based draft using instruction + summary
- sendReplyTool: uses EmailConnector.sendReply

All tools must have:
- zod schemas for inputs
- required permission levels (sendReply is SENSITIVE)
- emit log events

Then update InboxAgentScreen to call the agent runner with a plan.

Return full code.
```

---

# Hero Demo #2 — Lead / Appointment Agent

## Prompt 8 — Lead intake + appointment booking

```text
Build a new screen: LeadAgentScreen.

Requirements:
- A lead intake form: name, phone, email, service type, preferred time windows, notes
- On submit:
  - create a "lead" record in memory facts store
  - generate a follow-up SMS/email draft (mock)
  - optionally create a calendar event (CalendarConnector.createEvent)
- Show a simple pipeline view: New → Contacted → Booked
- Provide "Auto-Follow-Up" button that runs an agent plan:
  1) classify lead urgency
  2) draft message
  3) schedule follow-up reminder

No external services. Use mocked connectors + memory + logging.

Return full code and navigation wiring.
```

## Prompt 9 — Lead tools + pipeline logic

```text
Implement lead pipeline logic as reusable code in packages/agent-demos/leads (create this package if needed).

Include:
- lead types
- state machine transitions
- tools:
  - saveLeadTool
  - classifyLeadTool (rules-based)
  - draftFollowUpTool
  - createAppointmentTool
  - scheduleReminderTool (writes to memory facts)

Wire LeadAgentScreen to run an agent plan using these tools.
Return all code.
```

---

# Hero Demo #3 — Crypto Ops Weekly Treasury Report

## Prompt 10 — Crypto ops screen + mock data

```text
Build a new screen: CryptoOpsScreen.

Requirements:
- Store a mock "portfolio" in memory: holdings, cost basis, current price, notes
- A button "Generate Weekly Treasury Report"
  - creates a report with:
    - portfolio summary
    - PnL by asset
    - risk flags (concentration, high volatility)
    - suggested actions (DCA, rebalance) as "recommendations" (no trading)
- A button "Export Report" that outputs JSON and allows copy/share (basic).

Use a mocked PriceFeed connector (random-ish but deterministic) and logging.

Return full code + new package if needed.
```

## Prompt 11 — Report generator + scheduling hooks

```text
Create packages/agent-demos/crypto with:
- types
- mock price feed connector
- treasury report generator
- tools:
  - loadPortfolioTool
  - fetchPricesTool
  - computePnLTool
  - generateReportTool
  - saveReportTool (to memory facts)

Add a simple "weekly schedule" placeholder (store nextRun date in memory) and a UI toggle to enable it.
Return full code.
```

---

# Distribution Moat — Weekly Ship Log (content engine)

## Prompt 12 — Auto-generate weekly ship log

```text
Add a screen: ShipLogScreen.

Goal: turn internal logs + facts into a weekly post draft.

Requirements:
- Pull last 7 days of logs from packages/logging
- Pull last 7 days of facts from packages/memory
- Generate:
  - a short LinkedIn post
  - a Twitter thread (5-7 tweets)
  - a changelog bullet list
- Add "Copy" buttons.

No external LLM required: use deterministic templates + heuristics.
Return full code.
```
