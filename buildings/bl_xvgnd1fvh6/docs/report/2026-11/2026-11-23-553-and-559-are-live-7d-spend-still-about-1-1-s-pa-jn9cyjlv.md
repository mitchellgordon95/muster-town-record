---
id: "dc_gvjn9cyjlv"
type: "report"
state: "building"
title: "#553 and #559 are live; 7d spend still about 1.1 s; parked until after midnight to read the reset tick"
authorId: "ag_b7u4rlqgcz"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-23T16:50:49.066Z"
sessionId: "se_m7mv3fwj10"
assignmentId: "as_8fs6uo57oe"
costUsd: 0.5115446
tokens: 25577
turns: 13
createdAt: "2026-11-23T16:50:49.058Z"
updatedAt: "2026-11-23T16:50:49.066Z"
---
## What I did
I read /api/health at 16:49Z. Live is commit 6b32f5fe, started 16:46:38Z. `git merge-base --is-ancestor` confirms both 94ecde00 (#553) and 15697af4 (#559) are in it. They went live with Mitchell's 16:09Z redeploy, so no midnight has passed with them live yet. I timed GET /api/finance/spend?window=7d eight times. I also re-read the slow-tick code and the step 1–2 rows in docs/scaling.md.

## Findings
- **kr_un8kya36jl (spend under 500 ms): misses live.** Five timings at 16:50Z were 1.07, 1.14, 2.55, 1.24 and 1.12 s, median 1.14 s. Three more calls had a time to first byte of 0.94–1.06 s. For comparison, /api/health answers in 0.07–0.10 s, so the time is spent on the server. The response is 775 kB, and 742 kB of it is `rows`. The baseline before #559 was a median of 1.33 s ([dc_rrlhzg26fr](2026-11-22-verify-live-neither-pr-is-live-yet-and-midnight-ha-lhzg26fr.md)). Step 2 ([dc_3c1w31qmjm](2026-11-22-finance-and-goal-spend-read-agents-by-column-pr-55-1w31qmjm.md)) expected this. The retired-fork part is gone, and what is left is parsing all of history (sessions, debits, assignments) plus a large JSON response. No step of this grant covers that.
- **kr_wkpd11d50e (bench): half holds.** docs/scaling.md has the row. resetDaily p50 is 0.08 ms at 0 retired forks and 0.10 ms at 30,000. Both are under 1 ms, so the reset is flat. Tick p50 is 34 ms at 0 and 163 ms at 30,000, which is about 5×. So the tick half fails, as the step 2 report said: explore, work, needsBackstop and walkHome still scan every agent.
- **kr_a0mgj1zw7b (midnight reset under 100 ms): waits for 2026-11-24 00:00Z.** A caveat on the check: `load.tick.slow` keeps a tick only when it ran over 500 ms (SLOW_TICK_MS, packages/runtime/src/index.ts:722). It also keeps only the latest such tick. If the midnight tick is fast, it will not appear there. The plan when this resumes:
  1. Read /api/health load.tick.slow and load.tick.last.
  2. If the slow tick's `at` is after 00:00Z and has a `dailyReset` phase, use that number.
  3. If no slow tick since 00:00Z has a dailyReset phase, the midnight tick was under 500 ms. That meets the tick-under-1,000 ms half. The dailyReset value itself is then unknown live. The evidence for under 100 ms is the desk bench at 0.10 ms.
  4. Claim kr_a0mgj1zw7b with that. File kr_un8kya36jl and kr_wkpd11d50e as open with the numbers above. Rewrite the topic page Runtime tick cost ([dc_ur1qzaxafp](../../wiki/2026-11/2026-11-03-runtime-tick-cost-gr-db6ofyd0yf-1qzaxafp.md)), then close the step.

## What I need from you
Nothing needed.
