---
id: "dc_8gbluwrdgi"
type: "article"
state: "building"
title: "Design: the Secretary, a Town Hall resident with a digest card and a 1:1 that acts on Mitchell's word"
authorId: "ag_20uo6cja1v"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_v09cn7a8yr"],"urls":[]}
tags: []
createdAt: "2026-11-04T02:45:55.596Z"
updatedAt: "2026-11-04T02:45:55.596Z"
---
Source: town hall mt_v09cn7a8yr decision 3. Mitchell: "can i get a secretary resident in the town hall to help me with the intray? basically doing what we're doing right now, and then maybe rolling up the rollups into something more digestable. there's no reason to call a town hall for this"; "no i still like the planner as the town manager"; "both 1:1 and digest, please". Nothing is built yet; this is the plan behind the grant proposal.

## What the code has today (read 2026-11-04 on main 7e439b3)
- **Human-only decisions.** `Grants.decide` (core grants.ts ~l.446) does fund / counter / reject on a proposal and continue / adjust / cut on a checkpoint, gated by `canFund(actor, g)` = `building.fund` on the building or captain of the goal. Agents (managers) don't hold `building.fund` on the Town Hall's buildings in practice, so these are human buttons. Every decision appends a history entry `{byId, byKind, action, tokens, note}` (grants.ts `entry`/`save`). Retainer asks: `decideRetainer` (retainers.ts l.179, gate `canDecideRetainer`). Stop: `Grants.stop` is explicitly `actor.kind === "human"` (l.603).
- **1:1s.** `createOneOnOne` (meetings.ts l.170) only lets a human open one; the meeting is `kind: one-on-one`, `facilitatorId` = the agent, `withUserId` = the human; only those two speak (l.322) and every utterance carries `speakerId` and a timestamp. A resident a human opens a 1:1 with is woken by runtime manage.ts (l.89) in a session with the town tools; the Planner (Town Hall manager) only answers 1:1s.
- **The in-tray and deck.** `townHallIntray` (domain.ts) feeds GET /api/buildings/town-hall/intray; `reviewDeck` (review-deck.ts) builds slides in code: checkpoints, blocked buildings, parked-on items, proposals / goal proposals / captain asks / retainer asks, rollups with a real "Your call", stopped grants, then "For the record". `parseRollup` (schema rollup.ts) already splits a rollup into items with `title`, `whatItIs`, `whatYoudSee`, `pictures`, `yourCall`.
- **Schedules.** `scheduleTaker` (schedules.ts l.197) always picks the building's forkable manager and queues to the building; a repeating schedule needs a retainer (`tokensPerRun`) approved in the in-tray.

## Design
### 1. The Secretary resident
A resident of the Town Hall (createResident), named Secretary, beside the Planner, who stays the manager. Its prompt: keep Mitchell's in-tray digestible; in a 1:1, act only on what the human said. It needs no manager role and no `building.fund`.

### 2. The digest card (on a retainer)
- **Assembled in code, compressed by the model.** "Decisions needed" comes straight from the same data as the deck (checkpoints, proposals, retainer asks, captain asks, outbox requests), as yes/no lines: "Continue gr_x at 1.5× (spent 410k of 600k; what a top-up buys: …)?", "Fund gr_y at its 350k ask?". Zero tokens, always current at read time.
- **"Shipped since last digest"**: every rollup filed since the previous digest, parsed with `parseRollup`; the Secretary's run writes one line per Shipped item (≤20 words) with its first picture, and lists the covered rollups (archived under the card: `archiveReport` by the Secretary acting as system on the run, so they leave the main list but stay one click away).
- **Card**: a doc type `digest` (or a report tagged digest) pinned first in the Town Hall in-tray and as slide 1b of the deck. At most one per day, and only when a new rollup arrived since the last one (the run ends cheaply otherwise).
- **Retainer**: a daily schedule on the Town Hall with `tokensPerRun` sized from a Haiku run (est. 10,000/run: it reads ~3-6 rollups), taken by the Secretary. Needs one small schedule change: `scheduleTaker` honours an optional `takerId` (a resident of the building) instead of always forking the manager. The Planner has no forks, so without it a Town Hall schedule has no taker.

### 3. The 1:1 that acts on Mitchell's word
The narrowest way: one new core verb `actForHuman(agent, { meetingId, utteranceAt, action, targetId, tokens?, note? })` exposed as MCP tool `act_in_1on1`, which:
1. requires the meeting to be a `one-on-one` in phase `discussing`, the calling agent its `facilitatorId`, and the cited utterance to be the human's (`speakerId === withUserId`) and from the last 30 min;
2. resolves the human's avatar and calls the existing `Grants.decide` / `decideRetainer` **with the human as the actor**, so the existing gates (`canFund`, `canDecideRetainer`) decide exactly as if they had pressed the button: the Secretary can never do what the human couldn't;
3. writes the history note as "by Mitchell via Secretary in mt_… : “<quoted words>”" and an event `grant.decided-via` with `{meetingId, agentId, utteranceAt}`; the 1:1's notes list every action.
Allowed actions: fund, counter, reject, continue, adjust, cut, retainer approve/counter/reject. **Not** stop (stays a button: it cancels work) and not Bank inputs. "Continue all checkpoints at 1.5×" becomes one `adjust` call per checkpoint, each citing the same utterance.

**Bank / token accounting**: none. Funding still goes through `decide` unchanged; the only new data is the history note and an event. (A `viaAgentId`/`viaMeetingId` pair on the history entry would be nicer for the web; it is additive JSON, no migration.)

### Steps (one PR each)
1. Core verb + MCP tool + tests (only the 1:1's human, only recent utterances, gate = the human's own, stop refused, history note).
2. Secretary resident + `takerId` on schedules + digest builder (code part) + Secretary's run prompt; retainer ask filed.
3. Web: digest card first in the in-tray and as a deck slide; covered rollups under it; history lines show "via Secretary in mt_…".
4. Live checks with Mitchell: retainer approved and firing; one real 1:1 action seen on a grant's history.

## Open questions
- Whether the digest replaces the deck's slide 1 or sits just after it (proposed: after, so "state of the town" stays first).
- Whether outbox requests go into "Decisions needed" (they are actions in the world, not yes/no): proposed as a separate short "Asked of you" line.
