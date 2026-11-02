---
id: "dc_syd8drel26"
type: "report"
state: "building"
title: "Goal tree step 5 merged (PR #128, e3da989): Change this goal + Plan with an agent; live check parked"
authorId: "ag_sgnkblhiby"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_kh0zaqui0w","dc_k76m4lhs9a","dc_0xqyrevla1"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/128"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 5 merged as e3da989 (PR #128), no migration, no Bank code; live check as_taeogbf1al already resumed on the deploy. The Planner-payment question is a Bank decision reserved for Mitchell: it goes into rollup 33 Needs together with the steps 7-8 Bank yes, not to him directly. Step 6 (postmortems + kanban, not Bank-gated) queued behind the live check."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T23:52:30.810Z"
sessionId: "se_9l7yonjlgv"
assignmentId: "as_61yn0bp2x8"
costUsd: 6.653990999999998
tokens: 332700
turns: 92
createdAt: "2026-10-30T23:51:51.628Z"
updatedAt: "2026-10-30T23:52:30.810Z"
---
## What I did
The session started fine this time (no credential error). I built goal tree step 5 from docs/goals.md, ran `npm run check` (green locally and in CI) and merged PR #128 (https://github.com/mitchellgordon95/muster-town/pull/128) as **e3da989**. I queued a redeploy, so **e3da989 should be live**. The live check and the ≤300 px crop for rollup 33 are parked on that deploy. There is no migration (`goal_changes` came with 061; the highest migration on main is still 061) and no Bank code change.

## Findings
- **Change this goal** (core `goal-changes.ts`, `world.reorgs`). `POST /api/goals/:id/change` takes X → Y and a why, from an admin or the goal's owner, one open change per goal. It creates:
  - a human note at the Town Hall,
  - the `goal_changes` row,
  - one directed prep assignment per building attached under the goal (on its building queue, naming the `reorgId`),
  - "under review" on every open key result under the goal (grants keep running),
  - a Town Hall `planning` meeting. It opens when every prep report is in or after 24 h, whichever comes first (mt_kh0zaqui0w Q6). When nothing is attached under the goal it opens at once.
- **Meeting lifecycle.** When the meeting starts, the goal's text becomes Y. When it ends, the change is decided. `POST /api/key-results/:id/review` handles Keep / Move / Archive (archive = missed) for under-review key results. `propose_goal` / `propose_key_result` take `reorgId`, and the facilitator's prompt lists the change, the prep reports, the proposals and the under-review key results.
- **Plan with an agent.** The Planner is a Town Hall resident, created on first use. `POST /api/planner/one-on-one` opens a 1:1 with it. Its prompt carries the tree, scoped to the goal it was opened from. It drafts proposals that are filed under no building, and each proposal shows in the 1:1 as a card with Accept / Edit and accept / Cut.
- **Web.** The Goal tree gets "Plan with an agent" (in the header, on each row and in the goal detail), a "Change this goal" form with a status banner, and an "under review" pill with Keep / Move / Archive.
- **Tests.** Core `goals-step5.test.ts` (5 tests) and a runtime test where the Planner answers its 1:1 and proposes.
- **Gap: the Planner can't run live yet.** `bank.ts` `drawPool` gives the Town Hall nothing from the Bank, and docs/goals.md ties Planner payment to the Bank-gated step 7. Until that changes:
  - a Planner 1:1 posts a notice saying it can't start yet,
  - the reorg meeting falls back to the first manager invited (e.g. Pix) as facilitator.
  - Change this goal itself works without the Planner.
- **Left out:** a deck slide per undecided under-review key result, Cut candidates in the in-tray, the under-review flag on new grant proposals, and the Planner's first jobs.

## What I need from you
Decide how the Planner is paid before step 7: allow a one-line Bank change so the Town Hall's Planner draws from the General pool, or give the Town Hall an allocation.
