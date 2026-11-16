---
id: "dc_n4o5azb8fn"
type: "report"
state: "building"
title: "Step 2: ranks 6-10 fail loudly in draft PR #480; parked on its CI"
authorId: "ag_2gjss4l88k"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-16T18:54:47.049Z"
sessionId: "se_b5s95y2uvr"
assignmentId: "as_36czefa206"
costUsd: 2.5818695000000003
tokens: 129093
turns: 57
createdAt: "2026-11-16T18:54:47.029Z"
updatedAt: "2026-11-16T18:54:47.049Z"
---
## What I did
I fixed audit ranks 6-10 of [dc_0h2p8oiwy6](2026-11-15-fallback-audit-20-fallbacks-ranked-by-harm-10-to-f-2p8oiwy6.md) in one draft PR: https://github.com/mitchellgordon95/muster-town/pull/480. I added a test for each case and rewrote topic page [dc_fu5unwj1kr](../../wiki/2026-11/2026-11-15-fallback-audit-decision-5-5unwj1kr.md). I am parked on the PR's CI.

## Findings
- **Rank 6.** The gate facts now say "It gave no verdict" when the latest step report has none. Before, they said "continue".
- **Rank 7.** No path prices an unsized step as M any more. `askOf` refuses the step and names it. Forecasts skip unsized steps. The gate facts and the proposal need count them as "unsized". The web's `expectedSpend` and the step strip show them as unsized. One thing is kept, with a reason: the stored schema still allows a missing size. Grants funded before migration 098 have no sizes, and a back-fill would have to make one up.
- **Rank 8.** If the building no longer allows a step's model, `queueStep` holds the step and queues nothing. It writes a manager-level `step-held` entry on the grant's thread and a `grant.step-held` event. Topic pages that are gone are named in the step's description.
- **Rank 9.** A malformed MUSTER_TOWN_DATA_KEY now stops boot in main.ts. The secrets back-fill throws on it instead of returning 0.
- **Rank 10.** When the Planner can't run, the reorg meeting posts a notice. It names who facilitates instead and why, or says nobody can. There is no fallback to the Planner or to a stopped invitee.
- **Verified on my desk.** Typecheck is clean. All 1048 core tests and 432 web tests pass. A grep finds no `verdict ?? "continue"` and no `size ?? "M"` in packages/core/src. The pre-push fast check passed.
- **Key results.** kr_o57jr3l9kl can be claimed once #480 merges. kr_tjn739xi9g is already claimed, but its live-town check has not been run yet. Ranks 11-13 are not done; they were optional.

## What I need from you
Nothing needed.
