---
id: "dc_vxsq9g008a"
type: "article"
state: "building"
title: "Work routing: the target model"
authorId: "ag_9kbbtfr5je"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["mt_lsyqj98z0w","dc_4xww7x920l","dc_ktzj41hv8x","as_ukj2njrh9c"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/394"]}
tags: ["work-routing","architecture","mt_lsyqj98z0w"]
createdAt: "2026-11-08T03:43:05.700Z"
updatedAt: "2026-11-08T03:43:05.700Z"
---
# Work routing: the target model

Decided by Mitchell in 1:1 mt_lsyqj98z0w (2026-11-08): restructure work routing as a whole. Starts from the map [dc_4xww7x920l](2026-11-05-work-routing-the-map-ww7x920l.md) (21 paths, holes A/B/C/D). Step 1 is PR #394 (as_ukj2njrh9c).

## The model: two nouns

**For a human:** each building has an **in-tray** (the manager decides) and a **queue** (its workers do).

1. **A job** goes on a **building's queue**. Who runs it belongs to the building, not to the job: forks where the manager is a forkable resident; the manager itself where there are no forks (the Town Hall's Secretary, a lab resident named as schedule taker); a visitor as an **offer** (visitor-managed buildings, or a visitor named directly). Nothing addresses a forking manager as a worker.
2. **An in-tray row** goes to the building's manager and is handled in the team-lead session (as `managerIntrayRow`, core/src/wakes.ts:24), never as a work session: tells, @mentions and outbox answers aimed at a manager; grant countered / rejected; the manager's own parked session.

## In code after PR #394 (step 1)

`createAssignment` (core/src/domain.ts) takes no `queue` from its callers. Rule: named agent is a fork → its manager, building queue. Named agent is the forkable manager of its home building → building queue, unless `managerOnly: true`. Anyone else → its own queue (a visitor's is an offer). `managerOnly` is the bridge until step 2 and is used at exactly three call sites: grant countered/rejected (grants.ts `decisionAssignment`), a manager parking its own session (verbs/docs.ts park), and `retry` of an agent-queue row (ops.ts `retryAssignment`, "run it where it ran").

The checkpoint already creates **no** assignment on main (grants.ts `checkpoints`: "No assignment is created: the checkpoint card assembles itself"), so the map's row 14 needs nothing.

## The 21 paths: what each becomes

| # | Path | Before | After step 1 (PR #394) | Final (step 2) |
|---|---|---|---|---|
| 1 | `assign` no agentId | building Q | job, building Q (unchanged) | same |
| 2 | `assign` agentId = self (agent) / anyone (human) | manager's own Q | **job, building Q** when it names a forking manager; visitor → offer | same |
| 3 | REST `POST /agents/:id/work` | agent Q | **building Q** for a forking manager | same |
| 4 | `review` continue/redirect | #369: building Q via decisionQueue | building Q by createAssignment (decisionQueue no longer passed) | same |
| 5 | `review` continue on parked report | resumes in place | unchanged | same |
| 6 | Flag decided, assigneeId = manager | manager's own Q (test flags.test.ts:52) | **building Q** (test updated) | same |
| 7 | Meeting decision naming manager | #369: building Q | building Q by createAssignment; decisionQueue kept only for the decision line and skipping auto-approve | same |
| 8 | Amended-decision wake (wakes.ts decisionWakes) | manager's own Q | **building Q** | same |
| 9 | Park (`submit_report resumeWhen`) | fork → building Q; manager → own Q | fork → building Q; manager → own Q (`managerOnly`) | manager's park → in-tray row / resumed team-lead item |
| 10 | Tell relay to a manager / building id (relayWake) | manager's own Q ("Message from …") | **building Q** (a fork answers it) | **in-tray row** for the manager |
| 11 | @mention of a manager (mentionWake) | manager's own Q | **building Q** | **in-tray row** |
| 12 | Outbox answer to a manager (requestAnswerWake) | manager's own Q | **building Q** | **in-tray row**; a retired fork's answer → building Q, same chain (B2) |
| 13 | `retry` | building row → manager's own Q (A11) | same queue as the original | same |
| 14 | Grant checkpoint | (no assignment on main) | none | none: the card is the in-tray row |
| 15 | Grant countered / rejected | manager's own Q | own Q (`managerOnly`) | **in-tray row** (like continue/adjust/cut already are) |
| 15b | Grant funded | queues step 1 (`queueStep`) | building Q / visitor offer (unchanged) | same |
| 16 | Schedule fires, takerId = manager | manager's own Q (A10) | **building Q**; takerId = Secretary / lab resident → its own Q | same |
| 17 | Daily digest button | Secretary's Q | unchanged (Town Hall has no forks) | same |
| 18 | Explore tick | building Q | building Q (no `queue` passed) | same |
| 19 | Red main fix | building Q | building Q | same |
| 20 | KR missed → postmortem | building Q (visitor-managed: never runs, B3) | building Q; visitor manager → **offer** (B3 closed) | same |
| 21 | Reorg prep | as 20 | as 20 | same |

## The holes #369 left (Pix's list), and what closes each

- wakes.ts relayWake / mentionWake / requestAnswerWake → building Q in **PR #394**; become in-tray rows in **step 2**.
- ops.ts createWork (REST work) → **PR #394**.
- human `assign` agentId = manager → **PR #394**.
- schedule takerId = manager → **PR #394**.
- town-made manager jobs: checkpoint → none needed (no assignment on main); grant countered/rejected → `managerOnly` in PR #394, in-tray row in **step 2**.
- parked continuations: a fork's → building Q (already); a manager's own → `managerOnly` in PR #394, **step 2** decides.
- createAssignment default queue → gone in **PR #394** (no caller passes `queue`).

## What is lost

- A forking manager can no longer take a small blocking job itself (the AGENTS.md non-negotiable 1 wording and prompt rule C1 "assign a task to yourself only when small, blocking…"): `assign agentId=self` now queues it for a fork. Step 3 rewrites those lines.
- Flag `assigneeId = manager` and schedule `takerId = manager` mean the same as leaving them out.
- Until step 2, a tell or @mention to a manager is answered by a fork (one session per message), not by the manager in its team-lead session.
- `accept_assignment` / "New assignment from" message no longer goes to a manager naming itself.

## Migration order

- **Step 1 (PR #394):** createAssignment routes by building; `managerOnly` bridge; tests.
- **Step 2:** (a) relayWake, mentionWake, requestAnswerWake: when the recipient is a forking manager, write an in-tray row (a pending doc in its building's in-tray, the shape of `managerIntrayRow`) instead of an assignment; a retired fork's request answer → building queue on the same chain. (b) grants.ts `decisionAssignment` (countered/rejected) → in-tray row. (c) the manager's own park → decide: in-tray row that resumes in the team-lead session. (d) remove `managerOnly` and its three uses; (e) runtime/src/index.ts:602-620 (`work.residents` loop) skips forking managers, so no work session ever starts as a forking manager; a boot repair moves any pending agent-queue row of a forking manager to the building queue. Tests: wakes-relay, wakes-step5, lanes (countered/rejected), runtime scheduler.
- **Step 3 (docs):** architecture.md subsystem row :22 (lanes + two queues), diagram :31-52, :56-57, :98, :278, :289-291; docs/wakes.md :34, :41; invariants/assignments-lanes.md inv. 7 and 8 (one rule: work goes to a building); how-work-gets-done.md §6 and prompts.ts:206 ("never held for money" is wrong); AGENTS.md non-negotiable 1 and the team-lead prompt C1; add architecture.md's routing table to check:docs coverage.

