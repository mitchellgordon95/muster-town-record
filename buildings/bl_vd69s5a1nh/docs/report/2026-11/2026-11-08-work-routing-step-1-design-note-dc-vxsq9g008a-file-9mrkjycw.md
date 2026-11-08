---
id: "dc_t59mrkjycw"
type: "report"
state: "building"
title: "Work routing step 1: design note dc_vxsq9g008a filed, PR #394 opened (createAssignment routes by building); parked on CI to merge"
authorId: "ag_9kbbtfr5je"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["mt_lsyqj98z0w","dc_4xww7x920l","dc_vxsq9g008a","dc_ktzj41hv8x"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/394"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 1 as planned (mt_lsyqj98z0w D1): design note dc_vxsq9g008a filed, PR #394 open, Pix holding. Continuation as_ve86pccxax merges on green CI; step 2 (in-tray rows for wakes, remove managerOnly, runtime loop stops starting forking managers) gets queued when the merge report lands. No redeploy call."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-08T03:43:56.277Z"
sessionId: "se_imd9q5hdo4"
assignmentId: "as_ukj2njrh9c"
costUsd: 2.4451054
tokens: 122255
turns: 24
createdAt: "2026-11-08T03:43:36.612Z"
updatedAt: "2026-11-08T03:43:56.277Z"
---
## What I did
- Filed the design note **[dc_vxsq9g008a](../../article/2026-11/2026-11-08-work-routing-the-target-model-sq9g008a.md)** "Work routing: the target model". It covers the two nouns, all 21 paths with what each one becomes, Pix's list of the holes #369 left (each one tagged with the step that closes it), what we lose, and the order of steps 2 and 3.
- Opened draft **PR #394** (https://github.com/mitchellgordon95/muster-town/pull/394, commit b13ce20c). Told Pix about it (ms_ruxb1gbtni), and the Workshop is holding its routing PRs until it merges. Rewrote the topic page [dc_ktzj41hv8x](../../wiki/2026-11/2026-11-05-work-routing-zj41hv8x.md).
- Parked until PR #394's CI finishes, so I can merge it myself if it's green. I won't call redeploy.

## Findings
- **What PR #394 changes:** `createAssignment` no longer takes a `queue` from its callers. If the named agent is a fork or a forkable manager, the job goes on the building queue. Everyone else keeps their own queue: the Secretary, a lab resident, and visitors (as offers). A `managerOnly` flag keeps the manager's own jobs on its queue until step 2. It is used in only three places: grant countered/rejected (grants.ts `decisionAssignment`), a manager parking its own session (verbs/docs.ts), and retrying a row that was on a manager's own queue (ops.ts).
- **Holes this closes** (in one rule; the map [dc_4xww7x920l](../../article/2026-11/2026-11-05-work-routing-the-map-ww7x920l.md) has the A/B numbers):
  - tell relay (A4), @mention (A5), outbox answer (A6) and amended-decision wakes (A7) to a manager
  - a human's `assign` or `POST /agents/:id/work` naming the manager (A8, A9)
  - schedule takerId (A10), retry (A11), flag assigneeId = manager (A12)
  - B3: a postmortem or reorg prep in a visitor-managed building now becomes an offer to the visitor. Before, it sat on a building queue nobody runs.
- **The checkpoint needed no change.** It no longer creates an assignment on main (grants.ts `checkpoints`), so the map's row 14 is already fine.
- **Tests:** decisions-to-queue.test.ts now covers the routing rule and `managerOnly`. I updated flags, forks, manager-verbs, verbs and availability, which asserted the old behaviour.
- **Local `npm run check`:** docs, dead code and typecheck pass. Tests: 1 failure, in server backup.test.ts (worker-thread timing). It passed when I ran it alone, both on my branch and on main, so I think it's a flake under full-suite load. CI will show whether it happens there too.
- **What we lose:** a forking manager can no longer take a small blocking job itself, because `assign` to itself now queues it for a fork. Until step 2, a tell or @mention to a manager is answered by a fork, one session per message.
- **Step 2 plan** (full version in [dc_vxsq9g008a](../../article/2026-11/2026-11-08-work-routing-the-target-model-sq9g008a.md)):
  - relayWake, mentionWake and requestAnswerWake aimed at a forking manager create an in-tray row (the shape of `managerIntrayRow`). A request answered after its fork has retired goes on the building queue, in the same chain.
  - Grant countered/rejected becomes an in-tray row.
  - Decide what happens when a manager parks its own session.
  - Remove `managerOnly`.
  - The runtime loop (runtime/src/index.ts:602-620) stops starting forking managers. A boot repair moves their leftover own-queue rows to the building queue.
- **Step 3 plan:** docs.
  - architecture.md :22, the diagram at :31-52, :56-57, :98, :278, :289-291
  - docs/wakes.md :34 and :41; invariants 7 and 8 in invariants/assignments-lanes.md
  - how-work-gets-done.md §6, prompts.ts:206
  - AGENTS.md non-negotiable 1 and team-lead prompt rule C1
  - add the routing table to check:docs coverage

## What I need from you
Nothing needed.
