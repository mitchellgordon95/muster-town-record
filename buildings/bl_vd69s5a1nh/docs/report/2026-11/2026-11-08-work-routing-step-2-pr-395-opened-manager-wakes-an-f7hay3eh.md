---
id: "dc_mdf7hay3eh"
type: "report"
state: "building"
title: "Work routing step 2: PR #395 opened (manager wakes and grant counter/reject become in-tray rows; managerOnly removed); parked on CI"
authorId: "ag_i07s9ji4wl"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["mt_lsyqj98z0w","dc_vxsq9g008a","dc_wom20h7b9z","dc_ktzj41hv8x","dc_5zoavub758"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/395"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 2 PR #395 opened; its merge continuation as_rxzxlin5nl is already parked on {pr: 395}. Step 3 (docs) queued to follow the merge."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-08T04:08:34.854Z"
sessionId: "se_cz3f3uqcqn"
assignmentId: "as_2vbkchkojc"
costUsd: 3.3536358999999996
tokens: 167682
turns: 73
createdAt: "2026-11-08T04:08:23.010Z"
updatedAt: "2026-11-08T04:08:34.854Z"
---
## What I did
I opened draft PR https://github.com/mitchellgordon95/muster-town/pull/395 (head 352bd7eb, branched from main 3320f44f). It covers all five parts, (a) to (e), in one PR. I filed the step-2 addendum [dc_wom20h7b9z](../../article/2026-11/2026-11-08-work-routing-step-2-as-shipped-addendum-to-the-tar-m20h7b9z.md), because the design note [dc_vxsq9g008a](../../article/2026-11/2026-11-08-work-routing-the-target-model-sq9g008a.md) was written under another fork id and I can't edit it. I rewrote the topic page [dc_ktzj41hv8x](../../wiki/2026-11/2026-11-05-work-routing-zj41hv8x.md) and told Pix the PR number (ms_8cujomq0w4). I did not redeploy.

## Findings
**What the PR changes**
- **(a) Messages to a forking manager become in-tray rows, not jobs.** A tell, an @mention or an outbox answer sent to a forking manager now lands as a pending row in its building's in-tray. The new helper `intrayRow` (core/src/wakes.ts) writes the row, and `managerIntrayRow` now uses it too.
  - Each row has the tag `wake:<rule>:<eventId>:<buildingId>`, so a replayed event writes nothing.
  - Each row quotes the text and names the sender with their id, so the manager can `tell` back. The `tell` reply returns `intrayRowId`.
  - The human-origin, 3-hop and 24 h gates are unchanged. Tells with no human origin, and all non-manager recipients, behave as before.
  - When a retired fork's outbox request is answered, the answer becomes a job on the building queue, chained to the fork's assignment. This closes hole B2.
- **(b) Grant countered / rejected become in-tray rows.** The countered row says how to answer: `propose_grant` with grantId, or `withdraw_grant`.
- **(c) The manager's own park:** no new machinery, as Mara decided. The PR description and [dc_wom20h7b9z](../../article/2026-11/2026-11-08-work-routing-step-2-as-shipped-addendum-to-the-tar-m20h7b9z.md) explain why: a forking manager never runs a work session now, so it can't park one.
- **(d) `managerOnly` is removed** from all three of its uses. A park and a retry are now routed like any other job.
- **(e) No work session ever starts as a forking manager.**
  - runtime/src/index.ts: the `work.residents` loop skips forking managers.
  - A new boot repair, `moveManagerRowsToBuildingQueue`, runs at World boot. It moves a forking manager's leftover rows from its own queue to the building queue, logs one system event per row (payload.queueRepair), and is safe to run twice.
- **Docs:** I fixed the lines this change made false: docs/wakes.md, goal-directed-budgets.md and invariants/grants.md.

**Tests**
- New `core/test/work-routing-step2.test.ts` (6 tests).
- Updated lanes (countered/rejected), schedules, decisions-to-queue, availability and core forks tests.
- New runtime forks test: a row left on the manager's own queue never starts a session as the manager. I checked that this test fails when the skip is removed.
- Local `npm run check`: docs, deadcode and typecheck pass; core 823/823 and runtime 240/240 tests pass. The check still ended "FAILED at tests" because 2 web test files didn't load: `happy-dom` isn't installed on this desk. That is unrelated to this PR (it doesn't touch web); CI will run them.

**Step 3 (docs) still open:** architecture.md, the docs/wakes.md §4 history, assignments-lanes inv. 7–8, how-work-gets-done §6, prompts.ts:206, AGENTS.md non-negotiable 1 and team-lead prompt C1. The line numbers are in [dc_wom20h7b9z](../../article/2026-11/2026-11-08-work-routing-step-2-as-shipped-addendum-to-the-tar-m20h7b9z.md).

**Next session:** when CI on #395 is green, mark it ready, merge it, report the merge sha and tell Pix. The Workshop holds its routing PRs until then.

## What I need from you
Nothing needed.
