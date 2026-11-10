---
id: "dc_ejm1j7m3r8"
type: "note"
state: "building"
title: "Plan: the job abstraction (draft, inventory table unfinished)"
authorId: "ag_hinlwbx0c0"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_ewxnhs90cq","mt_db6itzy2br"],"urls":[]}
tags: []
createdAt: "2026-11-10T20:20:44.544Z"
updatedAt: "2026-11-10T20:20:44.544Z"
---
# Plan: the job abstraction (DRAFT, part B unfinished)

Source: Mitchell's 1:1s mt_ewxnhs90cq (18:35-19:39 UTC) and mt_db6itzy2br (20:11-20:16 UTC), decision as_qganrass1j. Read at main b12cc372. Status: sections A, C and D drafted; the inventory table B is partial (session hit the circuit breaker).

## A. The abstraction, as it will be built

### A1. One object: the job
A **job** is a row in a new `jobs` table: `id, buildingId, goalId, title, status, rule, pocketRef, createdBy, createdAt`.
- `status`: `proposed | countered | open | held | closed` plus `closedAs: done | cut | stopped | rejected | nothing-found | withdrawn`. One status machine for every job; today's grant statuses map onto it one to one (`checkpoint` = `held`).
- `rule` (the budget rule; replaces the lane):
  - `chunk` (today exploration): one Bank reservation of `exploreChunkTokens`; the job closes when its one session ends. `explore.ts` stays the starter tick and now creates a job of rule `chunk` instead of a bare exploration assignment.
  - `ceiling` (today grant): the grant row stays as the lifecycle object that holds the facts (steps with sizes, key results, ceiling, forecast); `jobs.pocketRef = gr_…`. Gate at 100% = `held`.
  - `per-run` (today retainer): the schedule stays as the lifecycle object (`pocketRef = sc_…`); each fire is one session on the job; the run cap is the schedule's `tokensPerRun`.
  - `pocket` (today directed): a human's pocket; `pocketRef` = the human source (`mt_…`, `ms_…`, flag doc). Never held for money, as today.
  - `building` (new, one per building): the manager's own thread (A2). No pocket of its own beyond the manager's wake cost, which is booked as today.
- A proposal is a job in status `proposed`. The explorer fork still files it itself (`propose_grant`): it creates the grant AND a new `ceiling` job; the explorer's own `chunk` job closes with an entry whose `moved.proposed = <new job id>` (the proposal is credited by code).

An **entry** is a row in a new `entries` table: `id, jobId, seq, authorKind (fork | manager | human | secretary | code), authorId, assignmentId?, sessionId?, pocket (the job's pocketRef at the time), tokens (adjusted, booked by the Bank as today), moved (json), proposes, answers (entry id it answers, nullable), level (code | manager | human | none), note, body (markdown), createdAt`.
- `moved` fields: `stepsDone: number[]`, `krClaimed: [{id, status, evidence}]` (today submit_report keyResults), `left: string` (NEW: what is left, one or two sentences, required on a `ceiling` job's step entry; the gate ask shows it), `topUp?: {tokens, buys}` (today), `proposed?: jobId`, `shipped?: [{whatItIs, whatYoudSee, picture}]` (close entries only; replaces the rollup's Shipped section).
- `proposes` = today's verdict: `continue | pivot | stop`, plus `close` (the work is done) and `nothing` (an explorer found no grant worth filing). The code maps it to an answerer level (A2).
- **The entry IS the report.** `submit_report` writes one entry on the session's job (its assignment carries `jobId`). There is no report doc, no rollup doc and no town-written in-tray row. The export renders each job's thread as one markdown file (`jobs/<id>.md`), so the git mirror keeps the record.
- Every session appends exactly one entry. A session that ends without one gets a `code` entry "ended without a report" (today the stub doc), answered at level manager.

### A2. One loop, three answerers
A job's last entry is **unanswered** until an entry with `answers = <it>` exists. `answer(entry)` in core runs on every new entry and decides the level:
1. **code** (always first, same transaction as the entry): `continue` on a `ceiling` job with steps left queues the next step (today grants.ts:574-578 `queueNextStep`); the forecast is computed and, past the ceiling, the entry is raised to level human with an ask (A3); a `chunk` job's `proposed` closes it and credits the proposal; `nothing` closes it; `stop`/`close` on a `pocket` job closes it; a `per-run` run entry closes the run (the schedule fires the next). The code's answer is itself an entry (`authorKind code`) so the thread shows what happened.
2. **manager** (only judgment): `pivot`; `close` on a `ceiling` job (the manager confirms the key results and closes the grant); the explorer's `proposed` (the manager reads the proposal before it goes up; it may withdraw or rewrite); a code entry the code cannot settle (session ended without a report, a failed resume). The manager answers with `review` on the entry: continue (queue its proposal), redirect (queue my words), close, stop, or **pass up** with a note. Approve-as-acknowledge on a mechanical entry is gone: those never reach the manager.
3. **human** at the nearest goal node above the building that has a human answerer (a captain, else Mitchell at the root): money (open a pocket, resize or close one), permission and the world (click, credential, request, meeting), rules. The human answers by deciding the ask; the decision is written as an entry (`authorKind human`, the label and their words) on the job's thread. Today those decisions become town-written in-tray rows (wakes.ts:40-54); they become entries the manager sees on the thread instead, and only wake the manager when the decision needs a manager move (counter, reject, cut, a key result flipped to missed).
- **Escalation spawns nothing.** "Pass up" sets the entry's level to the next answerer and attaches that level's note (`note`). That replaces the rollup's Needs section.
- **The manager's own words** across jobs are entries on the building's `building` job (A1). Its answerer is the human above. Shipped notices come from `close` entries' `moved.shipped`, not from a rollup.
- Queues are views, not tables: the manager's in-tray = unanswered entries at level manager in the building; a human's queue = open asks (A3) whose answerer node is theirs.

### A3. The ask
An ask is a question **rendered over a job's thread** plus the objects it references:
- facts from the lifecycle object (grant: ceiling, spent, steps by size, forecast; retainer: per run, runs left; request: what and who is parked),
- words from the manager's entry that raised it (`note`, `recommendation`) or from the Secretary, never a template,
- diff-first from the last entry on that job the human answered (`seen` table, today `seen.ts`).
Stored in the `asks` table (kept: rank, defer, history, claims and checks are the Secretary's queue mechanics) with two new required columns: `kind` and `sourceEntryId`.

Every ask is one of four `kind`s; today's `type` folds into it:
| kind | today's `type` | targets |
|---|---|---|
| `open` (open a pocket) | money on a proposed grant; money on an asked retainer | grant, retainer |
| `resize` (resize or close a pocket) | money: forecast past ceiling, checkpoint, raised retainer | grant, retainer |
| `act` (a thing only a human can do) | click, credential, meeting; outbox request; captain and access requests | request, captain, access, meeting |
| `rule` (set a rule) | policy (1:1 decision, Planner calibration, Secretary pattern) | rule |
Everything else is a **notice** (shipped, verified, closed loop, gate within ceiling, slate, pattern).

The recommendation of an ask comes from the entry that raised it (manager or Secretary). An ask with no recommendation from either is filed as **waiting on intake**: the Secretary of that answerer writes one or sends it back to the manager with a reason in words. Decision 5 (lint as warnings, PR #412, dc437530) stands: missing structure refused, style warns.

### A4. The goal tree is the chain
- One building per chain: walking up from any goal you meet a building once or never. One function, `chainConflict(goalId)` in `goals.ts`, returns the building above or below a goal, and every path that puts a building on a goal calls it (createBuilding, attach, adopt, goal move, goal add under a building's goal when the new goal would get its own building, collective import).
- A captain sits on a building's goal or above it, never strictly inside a building's subtree: `captain` request and captain set refuse such a goal.
- An intermediate node (a goal with no building on it and buildings below) has no jobs and no job status. It has a **pocket** (today's per-goal earmarks and caps), a **queue** (asks whose answerer node it is) and a **human answerer** (its captain, else the next captained node up, else Mitchell at the root).
- A boot audit lists today's violations as a notice and changes nothing (no live data is rewritten).

### A5. A Secretary per captain
- Each human answerer node gets a Secretary agent: same prompt, same verbs (rank, defer, slate, pattern, merge, send back with a reason = intake), scoped to the asks whose answerer node is theirs. Created when a captain request is accepted; stopped when the captaincy ends. No auto-secretary on a node without a captain.
- The root Secretary becomes the Town Hall's manager (Mitchell 18:49). The Planner stays a Town Hall resident and keeps `calibrate`.
- A resident may publish its own docs to its own building (`doc.write_building` for a resident on its home building).

### A6. The prompt cache constraint
The system prompt keeps only what is the same from one wake to the next (prompts.ts:463-467, docs/prompt-caching.md). Every new field lands as in the table in section D. The rule for the refactor: **a thread, a queue, an answerer's live state, an entry or an ask is first-message content; the fixed explanation of jobs, rules, levels and the four ask kinds is system prompt, byte-identical across wakes.** The test "a work session's prompt is split for the provider's cache" (packages/core/test/prompts.test.ts) gains a case per new block.

### A7. Stretch (plan only): mermaid inline
A fenced ```` ```mermaid ```` block in any markdown the web renders (Markdown.tsx `markdownHtml`) is drawn as a diagram, the library loaded lazily on first use. That covers docs, the meeting panel (an attached doc already shows inline, MeetingPanel.tsx:160 `Presented`) and ask bodies (AskCard renders markdown) without a new doc type. Cost: one S step in UI / UX. Not committed.

## B. Inventory table (NOT DONE this session)
The session hit the 500k circuit breaker while four read-only code inventories ran. The next session builds the full table (every object and path, file:line, new place or "retired"). Rows already verified by hand this session:
| Today | file:line | New place |
|---|---|---|
| `intrayRow` town-written in-tray report | packages/core/src/wakes.ts:35-54 | retired: human decisions become `human` entries (C step 5) |
| `queueNextStep` on step report | packages/core/src/grants.ts:574-578 | code answerer in `answer(entry)` |
| exploration tick | packages/core/src/explore.ts:1-8 | stays; creates a `chunk` job |
| `PROPOSAL_RECOMMENDATION` "Fund it: the building proposed it…" | packages/core/src/asks.ts:290 | retired; recommendation from raising entry or Secretary |
| `asksFromRollupProse` ("Your call" parser) | packages/core/src/asks.ts:445 | retired (C step 6) |
| rollup fold `foldRollup` / `fileRollupAsks` / `waitingRowIds` | packages/core/src/verbs/docs.ts:360-370 | retired (C step 7) |
| `doc.write_building` refusal for residents | packages/core/src/verbs/docs.ts:218; roles schema index.ts:293-295 | resident may publish to its home building (C step 2) |
| `overtakenReason`, `rollupCalls`, `settleRollup` | packages/core/src/secretary.ts:509, :560, :274 | retired with rollups |
| `ensurePlanner` as Town Hall agent | packages/core/src/goal-changes.ts:57, seed.ts:199, meetings.ts:189 | Secretary is manager; Planner resident |
| Boot repairs retitle/retype/foldTwin prose asks | docs/invariants/asks.md #12-14 | retired (C step 6) |
| "what is left" | no field today (grant-forecast.ts:63 computes sizes only) | `moved.left` on step entries |
| Markdown renderer / meeting attach | web Markdown.tsx:303, MeetingPanel.tsx:160, AskCard.tsx:147-148 | mermaid fence (stretch) |
| step size table S 50k / M 150k / L 400k | packages/schema/src/index.ts:75 | unchanged |
Still to inventory: submit_report verb and stub report (runtime), review verb, intray-routes, finance-manager-wakes, kanban, review-deck, rollup schema, notices emitters, every ask creator (grant-forecast.ts:88-96, grants.ts:897, retainers.ts:162, schedules.ts:184, docs.ts:494 outbox, captain.ts, access.ts, planner, policy), lanes.ts, direct.ts:43, entities.ts:28-50/226-233/262-263, goals.ts:421/436-441, goal-changes moves, permissions, web panels (RollupCards, Places in-tray, DecisionQueue, ReviewDeck).

## C. Migration sequence (PR-sized, in order)

Estimates are adjusted Bank tokens for the build session(s) plus the merge session (about 15k each, from the Workshop's own log: PR #412 cost 100k + 13k, PR #413 31k + 31k). The collective's step table is S 50k, M 150k, L 400k (schema index.ts:75). Every step is one PR, keeps the town running, and keeps `npm run check` green. Migration numbers start at 108 (highest on main is 107).

| # | PR | What changes | Retires | Size | Estimate |
|---|---|---|---|---|---|
| 0 | Lint decision 5 | Done: PR #412 merged dc437530 (style warns, structure refused). | three-tries path, lint pill | - | spent |
| 1 | Goal tree is the chain | `chainConflict(goalId)` in goals.ts; createBuilding, attach, goal move, collective import and `adopt` all call it; captain request and captain set refuse a goal strictly inside a building's subtree; boot audit files one notice listing violations; invariant in docs/invariants + tests. | the adopt-only check (entities.ts adopt refusal becomes the shared call) | M | 120k |
| 2 | Secretary manages the Town Hall; residents publish | Migration 108 swaps Town Hall manager to the Secretary, Planner stays resident with `calibrate`; `doc.write_building` for a resident on its home building; prompts updated. | Planner-as-manager special cases (`ensurePlanner` as Town Hall manager) | M | 130k |
| 3 | Jobs and entries, read only | Migrations 109-110: `jobs`, `entries`; `assignments.jobId` (nullable); back-fill: one job per grant (`ceiling`), schedule with a retainer (`per-run`), exploration assignment chain (`chunk`), directed chain (`pocket`), building (`building`); one entry per existing report doc (moved/proposes parsed from today's fields, body = the doc body), one per human decision event. `GET /api/jobs/:id` returns the thread. No behaviour changes; nothing reads entries yet. | nothing | L | 400k |
| 4 | submit_report writes the entry | `submit_report` appends the entry on its assignment's job (structured `moved`, required `left` on a ceiling step); `createAssignment` takes `jobId` and derives today's lane from the rule; explore.ts creates a `chunk` job; propose_grant creates a `ceiling` job in `proposed`. The report doc is still written beside the entry (one release) so the web and export keep working. | prose "what is left" | L | 350k |
| 5 | One loop: `answer(entry)` | The code answerer moves into one function (`queueNextStep`, forecast, proposal credit, nothing-found close, retainer run close); the manager in-tray becomes the unanswered entries at level manager; human decisions become `human` entries instead of `intrayRow` docs; `review` works on entries (continue, redirect, close, stop, pass up with a note); the team-lead wake fires on an entry at level manager. | `intrayRow` and its rules (wakes.ts:35-54), approve-as-acknowledge on step and exploration reports, "Session ended without a report" stub doc (becomes a code entry), report `decision` bookkeeping | L | 400k |
| 6 | Asks over the thread | `asks.kind` (open, resize, act, rule) and `asks.sourceEntryId` (migration 111, back-filled from type and sourceDocId); `renderAsk(ask)` builds title and body from the lifecycle object and the source entry, diff-first from `seen`; the recommendation comes from the raising entry or the Secretary; an ask with neither waits on intake. | `PROPOSAL_RECOMMENDATION` template (asks.ts:290), every town-written card text in grants.ts / grant-forecast.ts / retainers.ts / schedules.ts / docs.ts outbox / captain / access, the "Your call" prose parser (asks.ts:445 `asksFromRollupProse`, `proseAskShape`, `proseAskTitle`), the boot repairs `retitleProseAsks`, `retypeProseAsks`, `foldTwinProseAsks`, `retitleClippedAsks`, `overtakenReason` regex | L | 400k |
| 7 | The building thread replaces the rollup | The manager posts entries on its building's `building` job (`submit_report` with `rollup: true` becomes that); Shipped notices come from `close` entries' `moved.shipped`; Needs = entries passed up with a note; `close_grant` writes the close entry. | rollup schema and parser (schema rollup.ts), rollup typed-card fold (verbs/docs.ts:360-370 `foldRollup`, `fileRollupAsks`, `waitingRowIds`), rollup-asks.ts, `settleRollup`, the "Already waiting in your in-tray" line, RollupCards.tsx | L | 400k |
| 8 | A Secretary per captain | `asks.answererGoalId` (migration 112): the nearest captained goal up from the ask's building, else the root; `/api/asks` and the decision queue show a human only their node's asks (Mitchell: all); a Secretary agent per accepted captain with the same verbs scoped to its node; intake's "send back with a reason" verb writes a `secretary` entry answering the raising entry. | global-only ask queue | L | 350k |
| 9 | Delete the compatibility layer | Stop writing report docs; export renders threads; web reads entries (with UI / UX: the in-tray, review deck and grant pages read `/api/jobs`); docs (architecture.md, how-work-gets-done.md, legible-delegation.md, manual.md, invariants) rewritten to the job shape. | report docs as the record, `docs.decision` on reports, lane-specific prompt lines | L | 400k |
| 10 | Stretch: mermaid inline | Lazy-loaded mermaid in Markdown.tsx for ```` ```mermaid ```` fences (docs, meeting panel, ask bodies). UI / UX's step. | - | S | 50k |

**Total: about 3.0M adjusted tokens for steps 1-9** (about 3.05M with the stretch), plus about 15k per merge. Steps 1 and 2 are independent of 3-9 and can ship first. Steps 3-9 are a chain: each depends on the one before.

**Stop points.** After step 5 the town already has one loop and no ceremony approvals; after step 7 rollups are gone. If the cost runs past the forecast at step 5, stop there: steps 6-9 are the ask words and the clean-up.

## D. Where each new field lands under the prompt-cache rule (draft)
| New field or view | Lands in | Why |
|---|---|---|
| Fixed text: jobs, rules, entry fields, levels, the four ask kinds | system prompt (`workSystemPrompt` / `managerSystemPrompt`, prompts.ts:111, :470) | same on every wake |
| The session's job, its rule and pocket (replaces the lane line) | first message (`workStateBlock`, prompts.ts:189) | changes per assignment |
| The job's thread (last entries, diff from last answered) | first message (`chainBlock` successor, prompts.ts:334) | changes per session |
| Manager queue: unanswered entries at level manager | first message (`managerStateBlock`, prompts.ts:496; replaces `managerIntrayRows` :389) | changes per wake |
| Secretary's node queue, captain's name and node id | queue: first message; captain name and node id: system prompt (stable per Secretary) | per Secretary, stable |
| Ask render (kind, sourceEntryId, recommendation) | not in any agent prompt; the web and the Secretary's first message | live state |
| `moved.left`, `moved.shipped`, `proposes` | submit_report tool schema (static, cached with tool schemas) | schema only |
Each new block gets a case in prompts.test.ts "a work session's prompt is split for the provider's cache".

