---
id: "dc_joceqyqblp"
type: "report"
state: "building"
title: "gr_db6ofyd0yf step 3: live tick cost is the lane gate's free-token walk per queued item; PR #340 memoizes it per pass (desk 4× p95 1,225 → 330 ms), parked on CI"
authorId: "ag_ep66zn4hev"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Continuation as_vv75lxz36e waits on {pr:340}; the grant is at its checkpoint, so the merge-and-verify session is held until Mitchell continues/adjusts/cuts gr_db6ofyd0yf. PR #340 touches Bank read paths (memo of freeTokensAll / Bank.available per scheduler pass, no write path): the next rollup's \"Your call\" says so explicitly."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-04T19:25:09.742Z"
sessionId: "se_5azqqvglo2"
assignmentId: "as_34epfa6zt5"
costUsd: 2.7539630999999996
tokens: 137698
turns: 60
createdAt: "2026-11-04T19:24:43.961Z"
updatedAt: "2026-11-04T19:25:09.742Z"
---
## What I did
- Re-sampled the live tick: 30 samples on 0af48747 from 18:49 to 18:54Z, then more on later commits.
- Shipped sub-step timings in health `load.tick.last.sub` with PR #332. CI was green; I merged it as fd8558cc and it is live in 2adb84c2.
- Read the live attribution from those timings and profiled the 4× desk bench.
- Opened PR #340 (draft): one free-token walk and one `Bank.available` per scheduler pass, plus the before/after bench table in docs/scaling.md. https://github.com/mitchellgordon95/muster-town/pull/340
- Rewrote [dc_ur1qzaxafp](../../wiki/2026-11/2026-11-03-runtime-tick-cost-gr-db6ofyd0yf-1qzaxafp.md).

## Findings
**Live tick before the fix**
- Median 145 ms (range 97–445) over the 30 samples, 2–7 min after the 18:47Z boot.
- The work phase climbed from 40 to 280 ms as desk sessions started. Explore held ~32 ms. Streams was 1.25 ms, so that half of kr_0cbw6jb2p8 is met.

**Live attribution on 2adb84c2** (15 samples, 19:21–19:24Z, tick ~160 ms)
- work ≈ 95 ms. Of that, `work.forks.queue` is ≈ 76 ms: `forkableQueue` runs the lane gate on every queued building item, and each gate call repeats a ~17 ms `freeTokensAll` walk.
- explore ≈ 38 ms: `freeTokensAll` 17 ms + `block` 20 ms.
- So the step 2 "doubling" was queue length × walk, not the index.
- `exploreTick` itself already called `freeTokensAll` once per tick. The repeat walks were in `laneBlock` (grantDesk.exploration → goalFunding) and in `Bank.available`, which is the same global sum but was recomputed on every `canStart`.

**PR #340 fix:** `withTickMemo` around the explore, managers and work phases.
- `freeTokensAll` and `Bank.available` are computed once per pass.
- They are recomputed after any DB write (`total_changes()`) or when `now` moves by more than 1 s, so every answer equals a fresh computation.
- API reads are not cached.
- Tests pass locally: core 746, runtime 226, server 285, including the new tick-memo.test.ts.
- It touches Bank read paths for performance only. That is what this grant was funded for, and no write path changes.

**Desk bench, p50/p95 in ms** (kr_50wtkdofgc: ≤ 250 at 2×, ≤ 900 at 4×; table in docs/scaling.md)
| world size | before | after |
|---|---|---|
| 1× | 34/63 | 31/64 |
| 2× | 132/193 | 72/143 |
| 4× | 900/1,225 | 220/330 |

At 4×, work went from 632 to 104 ms and explore from 136 to 56 ms (p50). kr_50wtkdofgc is met on the PR branch.

**Expected live after #340:** work ~30 ms, explore ~25 ms, tick ~80–100 ms. That is not verified yet.

The next session merges on green and parks on the merge sha. Then it samples the live tick, re-checks the Bank figures (durable −907,734, credited 133,599,998), and closes the grant only if the live median is < 110 ms.

## What I need from you
Nothing needed.
