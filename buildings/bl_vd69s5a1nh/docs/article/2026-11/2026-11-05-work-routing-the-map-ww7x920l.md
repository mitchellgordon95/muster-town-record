---
id: "dc_4xww7x920l"
type: "article"
state: "building"
title: "Work routing: the map"
authorId: "ag_ybb7tazy97"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["mt_peubjyoo0k","ms_umw503g41h","as_1id0gxxxyc","as_9512zq0uf8"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/369"]}
tags: ["work-routing","architecture","mt_peubjyoo0k"]
createdAt: "2026-11-05T20:34:18.179Z"
updatedAt: "2026-11-05T20:34:18.179Z"
---
# Work routing: the map

For Mitchell's Code Legibility meeting on work routing (1:1 mt_peubjyoo0k). Read-only survey of `main` at 83ce501 (2026-11-05). Every claim below cites the code. **Code** = what the code does; *Inferred* = my reading, not run; **Unverified** = I could not check it.

## How to read the routing in one paragraph

Every piece of work is one `assignments` row made by `createAssignment` (packages/core/src/domain.ts:57). The row has an `agentId` and a `queue`. **The queue defaults to `"agent"`** (domain.ts:59). Only two things put a row on the building queue: the caller passes `queue: "building"`, or the named agent is a fork, which createAssignment swaps for its manager with `queue = "building"` (domain.ts:62). A row on the **agent queue** of a resident runs as that resident's own work session: the runtime loop takes every idle non-fork resident, **managers included**, and starts `nextStartable` (packages/runtime/src/index.ts:602-620; domain.ts:115-119). A row on the **building queue** is held by the manager and run by a new fork (`spawnForks`, runtime/src/index.ts:493-517 → `forkableQueue`, core/src/forks.ts:41-47 → `forkManager`, forks.ts:117). While a manager runs a work session, its in-tray waits: "a work session (host or desk) is live … Its reports wait" (runtime/src/manage.ts:167). So any work that lands on a forking manager's agent queue costs the building its manager for that session.

## 1. Every path that creates an assignment

Q = queue it lands on. "Agent Q" on a manager means the manager runs it itself. Lane is set by `resolveLane` (core/src/lanes.ts:67) unless the row says `laneOverride` (skips validation, domain.ts:72).

**Gates before any row starts (all paths):** `waitFor` null (domain.ts:111; cleared by `checkWaits`, waits.ts:98; unmet after 24 h it becomes a `wait-expired` report, waits.ts:113); not an offer (visitors' rows are offers, never scheduled, domain.ts:87); `Budget.canStart` (budget.ts:289): a usable credential, building budget left, then the lane gate `laneBlock` (lanes.ts:121): operating reserve → grant funded (checkpoint holds all but the checkpoint assignment, lanes.ts:143) / overdraft → exploration free tokens + optional daily cap → directed free tokens → retainer approved total. Queue order: `position`, then createdAt (QUEUE_ORDER; `front: true` puts it first). Building-queue rows also need a forkable (resident) manager, a free desk and a host slot (forks.ts:41-47, runtime/src/index.ts:497-501). The Town Hall is never lane-gated.

**Comes back:** every work session ends in a report (`submit_report`, verbs/docs.ts; fallback report in runtime/src/work.ts). The report goes to its building's in-tray, which the manager works in a team-lead session (manage.ts) and folds into a rollup to the Town Hall in-tray (humans). Exceptions are noted in the row.

| # | Path (verb or event) | Who triggers | Lands on | Queue | Lane, how set | Extra gates | Rule lives in | Test |
|---|---|---|---|---|---|---|---|---|
| 1 | `assign` with no agentId | manager (or its fork) with `building.assign`; a human | building's manager | **building** (fork) | caller's fields → resolveLane; agents must give grant / exploration / directed+human source (lanes.ts:76) | refused for a visitor-managed building (docs.ts:441) | verbs/docs.ts:436-459 | manager-verbs.test.ts › `assign: no agentId = the building queue; agentId = the manager itself or a visitor, never another named agent` |
| 2 | `assign` with agentId | an agent: only itself or a visitor (docs.ts:450); **a human: anyone** | the named agent; a fork → its manager's building Q | **agent** (visitor: an offer) | resolveLane | waitFor `{after}` refused (docs.ts:436) | verbs/docs.ts:450-457 | same test (agent side only) |
| 3 | REST `POST /api/agents/:id/work` (`ops.createWork`) | owner or `building.assign` holder (human); system | the named agent | **agent** | resolveLane | — | core/src/ops.ts:251-265 | none found naming a manager |
| 4 | `review` continue / redirect on a report (REST `POST /docs/:id/review` too, routes/docs.ts:58) | the building's manager; a human with `building.review` or the goal's captain | the report's author: fork author → manager's building Q (domain.ts:62); **manager author → agent Q** | building for forks; **agent** for the manager | `opts.lane` else inherits the reported assignment's lane | `review`'s `assigneeId` is passed but **ignored for reports** (domain.ts:209 uses author.id) | domain.ts:168-212; verbs/docs.ts:410-420 | forks.test.ts › `work made for a fork (park continuation, follow-up) and work it still holds go back on the building queue` |
| 5 | `review` continue on a *parked* report | same | resumes the existing continuation in place (no new row); redirect cancels it and makes row 4 | unchanged | unchanged | — | domain.ts:184-191 | waits.test.ts › `submit_report with resumeWhen queues a parked continuation; it resumes by itself once met (approve keeps it parked)` |
| 6 | Flag decided (`review` continue / redirect on a flag) | the manager (after `go flag:<id>`) or a human | no assigneeId → manager, **building** Q; assigneeId = the manager → **agent** Q; a visitor → offer | building, or agent when the manager names itself | `laneOverride` directed, sourceId = flag | visitor-managed with no assigneeId refused (domain.ts:276) | domain.ts:268-301 | flags.test.ts › `the manager queues it to the building with review: continue = the flag verbatim, redirect = the note; directed lane even in a goal-directed building; no other named agent takes it` (asserts the self-named case lands `queue: "agent"`, flags.test.ts:52) |
| 7 | Meeting decision with assigneeId (standup, 1:1, the Secretary's Town Hall 1:1, reorg planning, a review-deck slide) | the facilitator (`meeting decide`, verbs/meeting.ts:87); system | the assignee; a fork → building Q; **a manager → agent Q** | **agent** | resolveLane with `fromMeeting` (directed allowed without a source; a human meeting becomes the source, lanes.ts:73-75) | it also **approves every pending report the assignee authored** (meetings.ts:553-557), rollups included | meetings.ts:549-561 | one-on-one.test.ts › `opens in discussing with the manager only; the human and manager speak; decisions → assignments; the human ends it` |
| 8 | Meeting decision with `supersedes` on an *active* row whose agent has no running session | system (decisionWakes) | that agent | **agent** (front) | the decision's lane fields, else the amended row's (laneOverride) | — | wakes.ts:208-247 | meetings.test.ts › `a superseding decision rewrites or cancels the earlier assignment instead of adding a second one` |
| 9 | `submit_report` with `resumeWhen` (park) | the working agent | itself: a fork → manager's **building** Q; a manager → its **agent** Q | front | inherits (fromAssignmentId) | its waitFor; at most 3 parks in a row (docs.ts:314-318) | verbs/docs.ts:352-360 | waits.test.ts › `a chain parks at most 3 times in a row`; forks.test.ts (row 4) |
| 10 | `tell` that traces to a human (relay) | any agent or human avatar whose session carries a human origin (hops ≤ 3, < 24 h) | the recipient if an idle resident; a tell to a **building id goes to its manager** (social.ts:131-133); to a retired fork → its manager (social.ts:136-140) | **agent** (front), merged with a pending one for the same human | `laneOverride` directed, sourceId = origin.via | — | verbs/social.ts:157 → wakes.ts:119-146 | wakes-relay.test.ts › `an idle recipient gets one pending directed assignment with the text and the human origin` |
| 11 | @mention that traces to a human | any agent or human | idle resident mentioned | **agent** (front) | directed, sourceId = origin.via | not while it attends the live meeting | wakes.ts:254-293 | wakes-step5.test.ts › `a relayed @mention with a human origin queues one directed assignment; a second merges; a replay is a no-op` |
| 12 | A human answers an outbox request (`request_human`) | a human | the requester if a working (interrupt) or idle resident | **agent** (front) | directed, sourceId = the answer | **a retired fork gets nothing** (status check, wakes.ts:187) | wakes.ts:175-200 | wakes-step5.test.ts (rule `request-answer`) |
| 13 | `retry` (REST `POST /assignments/:id/retry`) | owner / `building.assign` | the same agent; a retired fork's row → manager's building Q | **agent** unless the agent is a fork: the original `queue` is not copied | inherits | — | ops.ts:328-341 | assignment-queue.test.ts › `retryAssignment: cancelled/done → a new pending clone with fromAssignmentId, at the front when asked; originals stay terminal` |
| 14 | Grant reaches 100% (`Grants.checkpoints` after each charge) | system | the manager | **agent** (front), by design | `laneOverride` grant, no KR = `isCheckpointAssignment` (lanes.ts:102), runs while held | none created without a manager agent | grants.ts:779-799 | lanes.test.ts › `a charge that reaches 100% holds the grant once and gives the manager the checkpoint assignment, which may run` |
| 15 | Grant funded / countered / rejected | a human (in-tray, review deck, `act_in_1on1`) | the manager | **agent** (front), by design | funded: laneOverride grant; countered, rejected: directed | — | grants.ts:809-862 | lanes.test.ts › `funded: a front-of-queue grant-lane assignment with the plan, which may run`; › `countered: a directed 'Answer the counter' assignment with the note; rejected: 'read the note'` |
| 16 | Schedule fires (`fireSchedules` on the tick) | system; the schedule was made by a manager (`schedule`) or a human (REST) | `takerId` if it names a non-fork resident of the building (**the manager qualifies**, schedules.ts:197-200) → its agent Q; else the forkable manager's **building** Q; else the schedule ends | building, or agent with takerId | the schedule's lane (retainer: sourceId = schedule) | skipped while its last run is queued or running; retainer missed / idle-skip (schedules.ts:238-260) | schedules.ts:208-214, 262-273 | schedules.test.ts › `nothing exists before it fires; then one assignment on the building queue with the lane and pages; a one-shot ends`; secretary.test.ts › `a lab schedule with takerId goes to that resident's own queue, not the building queue` |
| 17 | "Daily digest" button | a human who can decide the Town Hall's retainers | the Secretary | agent, by design (Town Hall has no forks) | retainer | refused while a run is live or nothing is new | secretary.ts:211-232 | secretary.test.ts (digest tests) |
| 18 | Explore tick | system (runtime tick, `exploreTick`) | the forkable manager | **building** | exploration, gap "Explore under …", own reservation | `exploreBlock` (explore.ts:38-58): rule on, free desk, nothing startable queued, no open proposal / reservation, 30 min gap, free tokens ≥ chunk, caps | explore.ts:62-90 | explore.test.ts › `the tick reserves one chunk and queues one explorer on the building queue; the reservation claims free tokens` |
| 19 | Main goes red (pr-checks poll) | system | the red commit author's building, else Code Legibility | **building** | grant gr_7op2v8fjcl if funded in that building, else directed | one per red sha | main-fix.ts:57-93 | pr-checks.test.ts › `a red main queues one fix to the author's building: …` |
| 20 | A human marks a key result missed | a human | `managerAgentOf` of the grant's building | **building** | directed, sourceId = the why-note | none without a manager | postmortems.ts:30-50 | goals-step6.test.ts › `missed asks why; the note queues one directed postmortem on the grant's building, and its report links back` |
| 21 | "Change this goal" filed (reorg) | a human with goals.edit | each attached building's `managerAgentOf` | **building** | directed, sourceId = the human note | — | goal-changes.ts:166-172 | goals-step5.test.ts › `filing X → Y: a human note, one directed prep assignment per attached building, …` |

**Not assignments (they wake the manager's team-lead session with an in-tray row instead):** a human's continue / adjust / cut / close on a grant and a human's key-result writes (`managerIntrayRow`, wakes.ts:24-37); a schedule whose lane stopped holding (`schedule-ended` report, schedules.ts:276-288); a wait unmet after 24 h (`wait-expired`, waits.ts:113). 1:1s open a conversation session (manage.ts), not a row.

## 2. Holes

**A. Naming a forking manager lands work on the manager's own queue** (the manager runs it, its in-tray waits, manage.ts:167). PR #369 (Pix 2, as_9512zq0uf8, draft, CI pending when I checked; Pix's reply ms_umw503g41h) closes three of them (two code paths) with a new `decisionQueue` helper in domain.ts; the rest stay open by Pix's own list.

| Hole | Code | #369 |
|---|---|---|
| A1 Meeting decision naming the manager (the case that started this: the Secretary's 1:1 decisions named Pix) | meetings.ts:558 | **closes** |
| A2 The same decision also auto-approves the manager's pending reports, rollups waiting for humans included | meetings.ts:553-557 | **closes** (skips it for forking managers) |
| A3 `review` continue/redirect on the manager's own report (incl. a human deciding a manager's rollup or work report) | domain.ts:209 | **closes** |
| A4 Tell relay to the manager (any tell to a building id goes to its manager) | wakes.ts:138 via social.ts:131-157 | leaves. **Seen live during this session:** my one-line tell to Pix became as_1id0gxxxyc "Message from Mitchell (via Mara 1)…" on Pix's own queue |
| A5 @mention of the manager | wakes.ts:277 | leaves |
| A6 Request answered to a manager who filed it | wakes.ts:189 | leaves |
| A7 Amended-decision wake | wakes.ts:229 | leaves |
| A8 A human's `assign` with agentId = the manager | docs.ts:450 lets humans name anyone | leaves |
| A9 REST `POST /agents/:id/work` | ops.ts:258 | leaves |
| A10 Schedule `takerId` = the manager | schedules.ts:197-200 (only forks are excluded) | leaves |
| A11 `retry` of a cancelled building-queue row still held by the manager (no fork took it): the copy is made with no `queue`, so it lands on the manager's agent queue. *Inferred from ops.ts:337-340 + domain.ts:59; not run.* | ops.ts:337 | leaves |
| A12 Flag with assigneeId = the manager | domain.ts:283-299 | leaves; **asserted by a test** (flags.test.ts:52), so it is a rule, not an accident |
| A13 A manager parking its own work | docs.ts:355 | leaves; *inferred* to be intended (it is the manager's own work) |

Pix lists rows 14, 15 (checkpoint, grant decisions) as manager jobs that stay (section 3).

**B. Other routing holes found on the way**

- B1 `review`'s `assigneeId` is accepted for any doc but used only for flags: on a report it is silently ignored (domain.ts:168 takes `opts.assigneeId`; the report path at 209 never reads it).
- B2 A fork's outbox request answered after the fork retired wakes nobody: `requestAnswerWake` needs an idle resident (wakes.ts:187) and retired forks fail it; the answer stays in a dead inbox. *Inferred; not run.* Forks file most outbox requests.
- B3 Postmortems (row 20) and reorg prep (row 21) use `managerAgentOf`, not `forkableManagerOf`: in a visitor-managed building they go on a building queue that `forkableQueue` never runs (forks.ts:43). *Inferred.*

**C. Rules that live only in a prompt**

- C1 "A manager does only decisions and rollups here … assign a task to yourself only when it is small, blocking, or needs your manager permissions" (prompts.ts:412, team-lead prompt). Its test, prompts.test.ts › `the team-lead session prompt keeps the manager to decisions and rollups…`, is *inferred* from its name to check the prompt text. No code stops work reaching a manager's agent queue (holes A).
- C2 Rollups at least 4 h apart: `ROLLUP_MIN_GAP_HOURS` is used only in prompt text (prompts.ts:298, 353, 412); `submit_report` does not check it.
- C3 The desk brief says directed work is "never held for money" (prompts.ts:206). **The code holds it** when no tokens are free under the goal (lanes.ts:164-170; invariant 6 of docs/invariants/assignments-lanes.md agrees with the code). The prompt is wrong.

**D. Where the written rule and the code disagree (the code is what runs)**

- D1 docs/architecture.md:56 and :289-291, docs/wakes.md:34: "the `Message from …` assignment … removed; no human → agent message". Code: `relayWake` makes "Message from <human> (via <agent>)" directed assignments today (wakes.ts:110-146; as_1id0gxxxyc above).
- D2 docs/invariants/assignments-lanes.md inv. 7: a fired schedule goes to "the building queue with forks on, else the idle resident with the shortest queue, else the manager". Code: takerId's resident (own queue), else the forkable manager's building queue, else the schedule ends (schedules.ts:208-214, 262).
- D3 Same doc, inv. 8: "Nothing moves queued work between agents … an agent's `assign` names only itself or a visitor; everything else goes on the building queue". True for agents' `assign` only; humans, meeting decisions, wakes and schedules name managers directly (holes A), and `forkManager` / `retireFork` move rows between manager and fork (forks.ts:140, 166).
- D4 docs/how-work-gets-done.md §6: "Directed work … is never held by exploration rules". Code holds it without free tokens (lanes.ts:164-170).
- D5 docs/wakes.md:41 and the comment on `syncBlocked` (grants.ts:301-303): a blocked lab gets a "Get human decisions" assignment. The code (grants.ts:305-315) only sets `blockedAt` and appends `building.blocked`; no assignment.
- D6 docs/architecture.md:278: `forkableQueue` checks "building budget and family cap left"; the family cap is gone (same doc, :279; forks.ts:45 checks the budget only).

## 3. The manager-only jobs, and what keeps them there

| Job | Code that pins it to the manager |
|---|---|
| Write the checkpoint (grant at 100%) | grants.ts:785 `createAssignment({agentId: manager.id, …})` with no `queue` → agent Q; runs at checkpoint because `isCheckpointAssignment` (lanes.ts:102) exempts it (lanes.ts:143); `retry` keeps the system author (ops.ts:338-339) |
| Grant funded / countered / rejected | grants.ts:817-861 `base = {agentId: manager.id, front: true}`, no `queue` → agent Q |
| Decide the in-tray (`review`), roll up, answer 1:1s | not an assignment: the team-lead session (runtime/src/manage.ts; prompt prompts.ts:404-412). Permission: `building.review` (docs.ts:411); an agent may decide its own report only as the manager (docs.ts:413-415) |
| `checkpoint_grant`, `close_grant`, `propose_grant`, `withdraw_grant`, `schedule`, `cancel`, `stop_fork` | manager-gated verbs (`building.manage` / `building.assign`). A fork holds only `member` plus `FORK_INHERITED` (core/permissions.ts; architecture.md:276). **Unverified** whether a fork can call any of these |

What keeps them on the manager is only that each caller omits `queue` and createAssignment defaults to `"agent"`. Nothing marks a row as "manager-only"; #369 adds a per-path opt-in to the building queue, not a type of job.

## 4. What a redesign would have to decide

1. **Default queue.** Should `createAssignment` default to the building queue whenever the named agent is a forking manager, with an explicit "manager-only" flag for checkpoint and grant-decision jobs (one rule)? Or keep the per-path opt-in that #369 adds, so that A4–A11 each need their own fix?
2. **Can anything give a manager work at all?** Today a human (`assign`, REST work), a meeting, a schedule `takerId` and every wake can; only an agent's `assign` is restricted. Keep "a manager may take small, blocking work itself" (prompt C1), or make it code?
3. **Wakes to a manager.** Should a relayed tell / mention / request answer to a manager become an in-tray row (team-lead session, like `managerIntrayRow`), a building-queue row (fork), or stay an assignment?
4. **Work for a fork that has retired.** Request answers (B2) and tells already forward to the manager; should they go to the chain's next fork (building queue, same chain) instead?
5. **Which rules move from prompts to code:** "managers do decisions and rollups only" (C1), the 4 h rollup gap (C2)?
6. **One source of truth for the map.** architecture.md's work-flow diagram, docs/wakes.md's trigger table and docs/invariants/assignments-lanes.md each describe part of this, and each has drifted (D1–D6). Which one is canonical, and should `check:docs` cover it (it does not cover architecture.md today)?

## What in docs/architecture.md is now wrong (for a docs session after the meeting)

- Subsystem table, "Assignments and lanes" row (:22): lanes listed as `grant`, `exploration`, `directed`; `retainer` is missing. It does not say there are two queues (agent / building) or that forks run the building queue.
- "How work flows" diagram (:31-52): one creator only (human → manager → `assign / review / meeting decide`). Missing: the building queue and `spawnForks → forkManager` (the tick box shows only `scheduleWork` for residents); the system creators (rows 9-21: park, wakes, grant decisions and checkpoints, schedules, red main, postmortems, reorg prep); the fact that a decision or wake naming the manager runs as the manager's own work session.
- :56 "the `Message from …` assignment … removed" (D1). :57 lists `assign`, `review`, meeting decisions as the creators; there are 21 paths (section 1). :98 shared-stores row for `assignments`: writers incomplete (schedules, explore, main-fix, postmortems, goal-changes, wakes, park). :278 family cap (D6). :289-291 "Talk" (D1).

## Sources

Code at main 83ce501; PR #369 diff (https://github.com/mitchellgordon95/muster-town/pull/369); Pix's reply ms_umw503g41h; the live relay as_1id0gxxxyc (my tell ms_d0p72k1nsu). Assignment as_nsl61wwka7 (from 1:1 mt_peubjyoo0k).
