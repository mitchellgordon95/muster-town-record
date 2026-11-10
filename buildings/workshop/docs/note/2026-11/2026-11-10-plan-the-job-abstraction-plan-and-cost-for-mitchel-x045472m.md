---
id: "dc_uwx045472m"
type: "note"
state: "building"
title: "Plan: the job abstraction (plan and cost, for Mitchell before any code)"
authorId: "ag_ur35rbd0a6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_ewxnhs90cq","mt_db6itzy2br","dc_kft2962dq9","dc_ejm1j7m3r8"],"urls":[]}
tags: []
createdAt: "2026-11-10T20:25:21.907Z"
updatedAt: "2026-11-10T20:25:21.907Z"
---
# Plan: the job abstraction

Sources: Mitchell's 1:1s mt_ewxnhs90cq (18:35-19:39 UTC) and mt_db6itzy2br (20:11-20:19 UTC), assignments as_qganrass1j and as_kuxyjwh6a3. This supersedes the draft [dc_ejm1j7m3r8](2026-11-10-plan-the-job-abstraction-draft-inventory-table-unf-m1j7m3r8.md). Code was read at main b12cc372, where the highest migration is 107. This is a plan and a cost. No code is written yet.

## Summary (one minute)

**One object: the job.** Every piece of work is a job: a grant, a retainer, an exploration chunk, a human's directed request, and each building's own thread. A job has one status machine and one budget rule (chunk, ceiling, per-run, pocket, building). Its record is a thread of **entries**, one per session plus the answers. An entry says what moved: steps done, key results claimed, **what is left** (a new field), top-up, a proposal made, what shipped.

**One loop.** Each new entry is answered at the lowest level that can settle it:
1. **Code** settles it when nothing needs judgment: it queues the next step, files the forecast, credits a proposal, closes a run.
2. **The manager** settles it when it needs judgment: a pivot, a close, a proposal to vet, a session that died.
3. **The human** at the nearest captained goal settles it when it needs money, permission or a rule.

Passing an entry up spawns nothing: it carries a note. Queues are views over unanswered entries and open asks, not separate documents.

**What goes away:**
- **Rollups.** No more rollup format, typed-asks list, prose parser, folding or "Already waiting" line. The manager's cross-job words become entries on its building thread. Shipped notices come from the close entries.
- **The town-written ask templates.** Six writers in asks.ts produce today's card words: proposal :272, retainer :307, request :323, captain :332, access :344 and the gate card :770. They are replaced by `renderAsk` over the job thread, which takes facts from the object and words from the entry or Secretary that raised the ask.
- **The "Your call" prose parser and its five boot repairs.**
- **Town-written in-tray report docs** (wakes.ts) and approve-as-acknowledge on mechanical reports.
- **Report docs as the record** (last step; the export renders threads instead).

**Cost.** 11 PRs, about **3.3M adjusted tokens**, or about 3.45M with merge sessions. The stretch item (mermaid) adds 50k. **Natural stop point after step 5b, about 1.7M including merges.** At that point the town has one loop and no ceremony approvals. Ask words and rollups are still the old ones. Steps 6-9 remove those.

**The one question for Mitchell:** should we build steps 1-5b now (about 1.7M) and decide steps 6-9 at that stop point with the cost known? The other option is to commit to the whole 3.45M now. Recommended: stop at 5b first.

## A. The abstraction, as it will be built

### A1. One object: the job

A **job** is a row in a new `jobs` table: `id, buildingId, goalId, title, status, rule, pocketRef, createdBy, createdAt`.

**`status`** is one of `proposed | countered | open | held | closed`, plus `closedAs: done | cut | stopped | rejected | nothing-found | withdrawn`. Today's grant statuses map one to one, with `checkpoint` becoming `held`.

**`rule`** is the budget rule, and it replaces the lane:
- **`chunk`** (today: exploration). One Bank reservation of `exploreChunkTokens`. The job closes when its session ends. explore.ts:142 `exploreTick` creates a `chunk` job.
- **`ceiling`** (today: grant). The grant row stays the lifecycle object, and `pocketRef = gr_…`. The job is held at 100%.
- **`per-run`** (today: retainer). The schedule stays the lifecycle object (`sc_…`). Each fire is one session, capped by `tokensPerRun`.
- **`pocket`** (today: directed). `pocketRef` is the human source (`mt_…`, `ms_…` or a flag). It is never held for money.
- **`building`** (new, one per building). This is the manager's own thread.

**Proposals.** A proposal is a job in `proposed`. `propose_grant` creates the grant and a `ceiling` job. The explorer's `chunk` job closes with `moved.proposed = <job id>`.

An **entry** is a row in a new `entries` table: `id, jobId, seq, authorKind (fork | manager | human | secretary | code), authorId, assignmentId?, sessionId?, pocket, tokens, moved (json), proposes, answers (entry id), level (code | manager | human | none), note, body, createdAt`.

**`moved`** holds:
- `stepsDone`
- `krClaimed` (today's keyResults)
- **`left`**: new, required on a `ceiling` step entry. No such field exists today; grant-forecast.ts:20 computes only sizes.
- `topUp`
- `proposed`
- `shipped[]` (close entries only)

**`proposes`** takes today's verdicts `continue | pivot | stop`, plus `close` and `nothing`.

**The entry is the report.** Every session appends exactly one entry. A session that dies gets a `code` entry, answered by the manager.

### A2. One loop, three answerers

`answer(entry)` in core runs on every new entry, in the same transaction:

1. **code** settles:
   - `continue` on a ceiling job queues the next step (today grants.ts `queueNextStep`, called from verbs/docs.ts submit_report).
   - Every step entry files the forecast. Past the ceiling, the entry is raised to human with a `resize` ask.
   - A chunk job's `proposed` credits the proposal. `nothing` closes the job.
   - `stop` or `close` on a pocket job closes it.
   - A per-run entry closes the run.
   - A report superseded by a meeting decision is settled (today meetings.ts:570 `applyDecision approve`).

   The code's answer is itself an entry.
2. **manager** settles: `pivot`, `close` on a ceiling job, an explorer's proposal, and code entries the code cannot settle. The manager answers with `review` on the entry: continue, redirect, close, stop, or **pass up** with a note.
3. **human** at the nearest captained node above the building (else Mitchell at the root) settles money, permission and the world, and rules. Their decision is written as a `human` entry on the thread. It wakes the manager only when a move is needed: counter, reject, cut, or a key result flipped to missed.

**Escalation spawns nothing.** Passing up sets the level and the note. This replaces the rollup's Needs section.

**Queues are views:**
- The manager's in-tray is the unanswered entries at level manager.
- A human's queue is the open asks at their node.

### A3. The ask

An ask is a question rendered over a job's thread:
- **Facts** come from the lifecycle object: ceiling, spent, steps, forecast, per run, runs left.
- **Words** come from the entry that raised it (`note`, `recommendation`) or from the Secretary, never from a template.
- It shows **diff-first** from the last entry the human answered (`seen.ts`).

The `asks` table is kept (rank, defer, history, claims and checks stay). It gains `kind` and `sourceEntryId`.

| kind | today's `type` and creator |
|---|---|
| `open` | money on a proposal (asks.ts:235 `askForProposal`), money on an asked retainer (:307) |
| `resize` | money from forecast or gate (:852 `askAtForecast`, :868 `askAtCheckpoint`) |
| `act` | click and credential for an outbox request (:323), captain (:332), access (:344), meeting |
| `rule` | policy: Planner calibration (planner.ts:183), ledger rule (secretary.ts:221 `proposeRule`, :261 `ruleFromOneOnOne`, :488 `filePattern`) |

Everything else is a notice. An ask with no recommendation from its raising entry or the Secretary waits on intake. Decision 5 stands (PR #412, dc437530): missing structure is refused, and style only warns.

### A4. The goal tree is the chain

There is one building per chain. A single `chainConflict(goalId)` is called by every path that puts a building on a goal: create, attach, adopt, goal move, collective import (rows in B5).

A captain sits on a building's goal or above it, never strictly inside a building's subtree.

An intermediate node has no jobs. It has a pocket (today's earmarks and caps), a queue and a human answerer.

A boot audit files violations as one notice and rewrites nothing.

### A5. A Secretary per captain

Each captained node gets a Secretary: the same verbs (rank, defer, slate, pattern, intake send-back) scoped to its node's asks. It is created when a captaincy is accepted and stopped when the captaincy ends.

The root Secretary becomes the Town Hall's manager. The Planner stays a resident with `calibrate`. Residents may publish to their home building.

### A6. Prompt cache

The fixed explanation of jobs, rules, levels and the four ask kinds goes in the system prompt. Threads, queues, entries and asks go in the first message. The table is in D.

### A7. Stretch: mermaid inline

A ```` ```mermaid ```` fence is drawn by Markdown.tsx, lazy-loaded. It covers docs, meeting attachments and ask bodies. One S step, done by UI / UX.

## B. Inventory (file:line at b12cc372 → new place)

Paths are under packages/. "(step N)" is the C step that moves or deletes it.

### B1. Writers of ask words (every `createAsk` call)

| Today | file:line | New place |
|---|---|---|
| `createAsk` (fold by target) | core/src/asks.ts:60 | kept; adds `kind`, `sourceEntryId` (step 6) |
| Proposal card: `askForProposal`, `proposalCard`, `PROPOSAL_RECOMMENDATION` | asks.ts:235, :272, :290; fired by `onGrantEvent` :229 from grants.ts:1081 | `open` ask rendered from grant + explorer entry; template retired (step 6) |
| `setAskCard` (explorer's own card) | asks.ts:296; verbs/grants.ts:44 | becomes the raising entry's words (step 6) |
| Retainer card `askForRetainer` | asks.ts:307; retainers.ts:162 | `open` ask over the per-run job (step 6) |
| Outbox request card `askForRequest` (credential/click regex) | asks.ts:323; verbs/docs.ts:496 | `act` ask; words = the request's own (step 6) |
| Captain card `askForCaptain` | asks.ts:332; captain.ts:36 | `act` ask at the goal's answerer node (step 6, routed in step 8) |
| Access card `askForAccess` | asks.ts:344; access.ts:58 | `act` ask at the root (step 6) |
| Gate card `gateCard` / `fileGateAsk` / `askAtForecast` / `askAtCheckpoint` / `retireGateAsk` | asks.ts:770, :830, :852, :868, :857; grant-forecast.ts:94, :101; grants.ts:897 | `resize` ask raised by the code answerer; shows `moved.left` (steps 5, 6) |
| Calibration policy ask | planner.ts:183 | `rule` ask, Planner's words (only kind added) |
| Ledger rule asks `proposeRule`, `ruleFromOneOnOne`, `filePattern` | secretary.ts:221, :261, :488 | `rule` asks, Secretary's words (only kind added) |
| Rollup typed asks `checkRollupAsks` / `fileRollupAsks` | asks.ts:386, :412; verbs/docs.ts:309, :368 | retired: pass up with a note on an entry (step 7) |
| Rollup prose parser `asksFromRollupProse`, `proseAskShape`, `MONEY_CALL`, `POLICY` regexes | asks.ts:446, :439, :431, :420; verbs/docs.ts:372 | retired (step 6) |
| Boot `backfillAsks` | asks.ts:477; world.ts:300 | kept for open items; drops its rollup-prose line :489 (step 6) |
| Boot repairs `retitleClippedAsks`, `retitleGrantAsks`, `retitleProseAsks`, `retypeProseAsks`, `foldTwinProseAsks` | asks.ts:564, :588, :624, :649, :686; world.ts:302-309 | retired (step 6); invariants/asks.md #12-14 rewritten |

### B2. Writers of in-tray rows (manager-facing items)

| Today | file:line | New place |
|---|---|---|
| `intrayRow` (a town-written pending report doc) | core/src/wakes.ts:40 | retired (steps 5, 5b) |
| `managerIntrayRow`: grant continued, adjusted, cut or closed; kr created, edited, moved or marked (`describe`) | wakes.ts:29, :64; runtime/src/waker.ts:76 | `human` entry on the job thread; wakes the manager only for cut or missed (step 5) |
| Counter / reject rows `decisionAssignment` | grants.ts:928-946 | `human` entry at level manager on the proposed job (step 5) |
| Relay of a human's tell `relayWake` | wakes.ts:143-160 | `human` entry on the building job (step 5b) |
| Outbox answer `requestAnswerWake` | wakes.ts:212-230 | `human` entry on the job that asked, else the building job (step 5b) |
| Meeting decisions `decisionWakes` | wakes.ts:268; meetings.ts:584 | `human` entry on the building job or the named job (step 5b) |
| Mention row `mentionWake` | wakes.ts:315; mentions.ts:86 | entry on the building job (step 5b) |
| Report doc from `submit_report` | verbs/docs.ts:266-450 | entry on the session's job; doc kept beside it until step 9b (step 4) |
| "Session ended without a report" stub | runtime/src/work.ts:151; prompts.ts:72 `FALLBACK_REPORT_PREFIX`; forks.ts:297 | `code` entry at level manager (step 5) |
| Flags `plantFlag` / `decideFlag` | domain.ts:236ff | a flag opens a `pocket` job; its first entry is the human's (step 5) |
| `applyDecision` (approve/continue/redirect/stop, parked, cancel next step) | domain.ts:174-226; verbs/docs.ts:455 `review` | `review` on an entry; approve-as-acknowledge gone for mechanical entries (step 5) |
| Manager prompt rows `managerIntrayRows` + in-tray rules | prompts.ts:174, :389, :412, :523 | queue-view block + fixed rules (steps 5, 7; see D) |
| Routing of items to a human `intrayRoutes` | core/src/intray-routes.ts:18 | `answererGoalId` on asks (step 8) |
| Manager wake on report/flag created | runtime/src/waker.ts (doc.created report/flag match) | wake on an entry at level manager (step 5) |

### B3. Readers of rollups

| Today | file:line | New place |
|---|---|---|
| Rollup format and parser `ROLLUP_SECTIONS`, `parseRollup`, `rollupAsks` | schema/src/rollup.ts:9, :85, :139 | retired (step 7) |
| Rollup submit: format check, Needs refusal, `rollupWaitingLine`, `waitingForHuman`, closed-grant link | verbs/docs.ts:287-330, :427, :442 | entries on the building job; `close_grant` writes the close entry (step 7) |
| Fold `foldRollup`, `waitingRowIds`, `rollupAsksFor`, `withAsks` | core/src/rollup-asks.ts:14-54 | retired (step 7) |
| Shipped notices `shippedNotices` | notices.ts:50 | from `close` entries' `moved.shipped` (step 7) |
| Secretary readers `settleRollup`, `overtakenReason`, `rollupCalls` | secretary.ts:274, :509, :560 | retired (step 7) |
| Review deck rollup slides, `rollupHistoryLine`, "approve rollups for the record" | review-deck.ts:72, :266ff; web ReviewDeck.tsx:72 | deck = asks + notices over threads (step 9a) |
| Close report link `checkpointDocId` | grants.ts:843-845; verbs/grants.ts:63-71 | the close entry id (step 7) |
| Manage session end `rollupId` | runtime/src/manage.ts:329-333 | entry id on the building job (step 7) |
| Web `RollupCards`, `rollupCardsOf` in DocView, rollup pill, `RollupAsks` row line | web panels RollupCards.tsx; DocView.tsx:15, :127; intrayList.tsx:26; Places.tsx:151 | thread view (step 9a) |
| Prompt: rollup rules, `ROLLUP_MIN_GAP_HOURS`, `escalationCriteria` | prompts.ts:357-364, :412, :523 | fixed "pass up with a note" rule (step 7) |

### B4. Budget rules (one per lane today)

| Today | file:line | New place |
|---|---|---|
| `laneBlock` / `laneHold` (reserve, grant funded/held/overdraft, retainer, reserved, exploration cap/free, directed free) | core/src/lanes.ts:108-166 | `ruleBlock(job)`: the same checks keyed by rule (step 4) |
| `resolveLane` (lane from human source) | lanes.ts:67 | picks or creates the job; lane derived from its rule (step 4) |
| Exploration chunk `exploreTick`, `startExplorer`, `closeReservations`, `exploreBlock` | explore.ts:142, :62, :87, :38 | creates and closes `chunk` jobs (step 4) |
| Free tokens and caps `freeTokens`, `exploreCapAt`, `claimShort` | free-tokens.ts:212, :42, :196 | unchanged; they are the node's pocket |
| Retainer `retainerHold`, `retainerClaim`, `watchRetainerRuns` | retainers.ts:238, :79, :251 | `per-run` rule check (step 4) |
| Grant gate: checkpoint at ceiling, forecast | grants.ts:897; grant-forecast.ts:20-101 | `ceiling` rule; the code answerer raises `resize` (step 5) |
| Step size table S 50k / M 150k / L 400k | schema/src/index.ts:75 | unchanged |
| Finance rows by lane | finance-lane-kind.ts | by rule, lane kept as an alias (step 9b) |
| Circuit breaker | circuit-breaker.ts:26 | unchanged (per session) |

### B5. Chain and captain paths (A4)

| Today | file:line | New place |
|---|---|---|
| `createBuilding` | entities.ts:28 | calls `chainConflict` (step 1) |
| `adopt` lab check (the only chain check today) | entities.ts:226-263 | becomes the shared `chainConflict` (step 1) |
| Attach `attach` / `setAttachment` | goals.ts:409-432 | calls `chainConflict` (step 1) |
| Goal create under a building's goal | goals.ts:241 | allowed (it is the building's work) |
| Goal move (accepted proposal) | goal-changes.ts | calls `chainConflict` (step 1) |
| Collective import | import-v0.ts:34 | calls `chainConflict` (step 1) |
| Captain request and captain set | captain.ts:20-27; goals.ts:261 `setOwner` | refuse a goal strictly inside a building's subtree (step 1) |
| `ensurePlanner` as Town Hall manager | goal-changes.ts:57; seed.ts:199; meetings.ts:189 | Secretary is manager (step 2) |
| Resident publish refusal | verbs/docs.ts:218 | allowed on its home building (step 2) |

**Unmapped (minor, handled inside step 9):** kanban.ts (queue board by lane), forks.ts:268 (spend by family), finance-manager-wakes.ts (counts decided docs), web DecisionQueue.tsx, GoalsTab.tsx, state.ts:316 wording, mock fixture.ts.

## C. Migration sequence (PR-sized, in order)

Estimates are adjusted Bank tokens per build. Each merge costs about 15k more (Workshop log: PR #412 cost 100k + 13k, PR #413 31k + 31k). Step sizes are S 50k, M 150k, L 400k. Every step keeps `npm run check` green and the town running. Migrations start at 108.

**What changed since the draft.** B turned up four things the draft missed:
- **Step 5b:** four more in-tray writers (relay, outbox answer, meeting decisions, mentions).
- **Step 9 split into 9a and 9b:** the web reading of rollups and the deck is bigger than one L.
- **Step 4 grows to 400k:** `laneBlock` and `resolveLane` are the lane's real home.
- **Step 1 grows a little:** the import and goal-move paths.

| # | PR | What changes | Retires | Size | Est. |
|---|---|---|---|---|---|
| 0 | Lint decision 5 | Done: PR #412, dc437530 | lint pill | - | spent |
| 1 | Goal tree is the chain | `chainConflict` called by createBuilding, attach, adopt, goal move, import; captain refusal; boot audit notice; invariant + tests | adopt-only check | M | 130k |
| 2 | Secretary manages the Town Hall; residents publish | migration 108; resident `doc.write_building` on its home | Planner-as-manager | M | 130k |
| 3 | Jobs and entries, read only | migrations 109-110; back-fill jobs from grants, retainers, chains and buildings, and entries from report docs and decision events; `GET /api/jobs/:id` | nothing | L | 400k |
| 4 | submit_report writes the entry; rules replace lanes | entry with `moved` (required `left` on ceiling steps); `ruleBlock(job)` replaces `laneBlock`; `resolveLane` picks the job; explore and propose create jobs; report doc still written | prose "what is left" | L | 400k |
| 5 | One loop: `answer(entry)` | code answerer (next step, forecast → `resize`, proposal credit, run close, meeting supersede); manager queue = unanswered entries; `review` on entries with pass up; grant and kr decisions and counter/reject become `human` entries; dead session = `code` entry | `managerIntrayRow`, counter/reject rows, stub doc, approve-as-acknowledge | L | 400k |
| 5b | Messages on the building thread | relay, outbox answer, meeting decision and mention become entries on the building job (or the named job); `intrayRow` deleted | `intrayRow`, relay/request-answer/decision/mention rows | M | 150k |
| — | **Stop point** | **about 1.61M + about 105k merges = about 1.7M** | | | |
| 6 | Asks over the thread | `kind`, `sourceEntryId` (migration 111); `renderAsk`; intake for asks with no recommendation | six card templates, prose parser, five boot repairs | L | 400k |
| 7 | Building thread replaces the rollup | manager entries on the `building` job; shipped from close entries; close_grant writes the close entry | rollup.ts, rollup-asks.ts, rollup submit path, Secretary rollup readers, rollup prompt rules | L | 400k |
| 8 | A Secretary per captain | `asks.answererGoalId` (migration 112); scoped queues; a Secretary per captain; intake send-back entry | global-only queue, `intrayRoutes` | L | 350k |
| 9a | Web reads threads | in-tray, review deck, grant page, doc view read `/api/jobs` (with UI / UX) | RollupCards, rollup deck slides | L | 400k |
| 9b | Delete the compatibility layer | stop writing report docs; export renders `jobs/<id>.md`; finance by rule; docs rewritten | report docs as record, lane prompt lines | M | 150k |
| 10 | Stretch: mermaid | lazy mermaid in Markdown.tsx | - | S | 50k |

**Total: about 3.31M for steps 1-9b, plus about 165k merges, about 3.45M.** With the stretch it is about 3.5M.

Steps 1 and 2 are independent and can ship first. Steps 3-9b are a chain.

**Stop point after 5b, about 1.7M.** At that point there is one loop, no ceremony approvals, and "what is left" on every step. Rollups and template asks still run alongside. If step 5 runs past its estimate, stop there.

## D. Where each new field lands under the prompt-cache rule

| New field or view | Lands in | Why |
|---|---|---|
| Jobs, rules, entry fields, levels, four ask kinds, the pass-up rule | system prompt (`workSystemPrompt` prompts.ts:111, `managerSystemPrompt` :470) | same on every wake |
| The session's job, rule, pocket (replaces the lane line) | first message (`workStateBlock` :189) | per assignment |
| The job's thread (diff from last answered) | first message (`chainBlock` successor :334) | per session |
| Manager queue: unanswered entries at level manager | first message (`managerStateBlock` :496; replaces `managerIntrayRows` :389) | per wake |
| A Secretary's node queue / its captain and node | first message / system prompt | live / stable |
| Ask render | web and the Secretary's first message only | live |
| `moved.left`, `moved.shipped`, `proposes` | submit_report tool schema | static |

Each new block gets a case in prompts.test.ts "a work session's prompt is split for the provider's cache".

