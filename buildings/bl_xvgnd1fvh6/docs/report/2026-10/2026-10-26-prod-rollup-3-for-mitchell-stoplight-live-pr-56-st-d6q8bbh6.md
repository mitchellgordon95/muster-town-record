---
id: "dc_uvd6q8bbh6"
type: "report"
state: "building"
title: "Prod rollup #3 for Mitchell: stoplight live (PR #56), stress-test grant drafted and waiting on the Prod key result; one thing only you can do"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_cyyb14f5ep","dc_gyb534k54l","dc_cr4bhpwhf3"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "let's do load testing on a throwaway first, i don't want to break stuff that's running"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-26T15:45:44.609Z"
sessionId: "se_80ap17bplm"
createdAt: "2026-10-26T15:21:12.283Z"
updatedAt: "2026-10-26T15:45:44.609Z"
---
## Shipped
- **Building stoplight, live** (PR #56, merged deabe02, verified live on 9b20fad; now on 119bd70): every goal-directed building shows a green / yellow / red lamp on its map banner and at the top of its board, with the reason on hover. Green = a funded grant on every key result; yellow = a key result without a funded grant, or a grant held at checkpoint; red = no key results, or no funded grant at all. Open-mode buildings (Prod today) and the Town Hall show no lamp. Reports: [dc_cyyb14f5ep](2026-10-26-stoplight-shipped-pr-56-merged-deabe02-green-yello-yb14f5ep.md) (shipped), [dc_gyb534k54l](2026-10-26-deabe02-pr-56-verified-live-on-9b20fad-the-worksho-b534k54l.md) (live check, read-only, zero writes to the server). Cost of the feature: 4.3 M tokens across the killed session and the retry.
- **Stress-test grant, drafted, not filed** ([dc_cr4bhpwhf3](2026-10-26-stress-test-grant-drafted-and-ready-to-file-dc-x4t-4bhpwhf3.md), draft [dc_x4twxh1a8o](../../note/2026-10/2026-10-26-stress-test-grant-the-proposal-as-filed-throwaway-twxh1a8o.md)): the full proposal from town-hall decision 3 (objective, approach, stop condition, ask 10 M tokens ≈ $15, five testing-plan lines, abort rule). It cannot be filed because `propose_grant` requires a Prod key result and Prod has none (`keyResults: []`). The continuation re-checks at 22:00 UTC today and files it in one call once the key result exists.

## Decided
- [dc_cyyb14f5ep](2026-10-26-stoplight-shipped-pr-56-merged-deabe02-green-yello-yb14f5ep.md) (stoplight shipped) → approved; the parked live check ran on the deploy.
- [dc_gyb534k54l](2026-10-26-deabe02-pr-56-verified-live-on-9b20fad-the-worksho-b534k54l.md) (deabe02 verified live) → approved; nothing further.
- [dc_cr4bhpwhf3](2026-10-26-stress-test-grant-drafted-and-ready-to-file-dc-x4t-4bhpwhf3.md) (stress-test grant drafted) → approved; the parked continuation as_iv8fk97gf8 already covers the next step, so no new assignment. The ask is below.

## Key results
- Prod has no key results and no grant (budgetMode open, General pool). Stoplight for Prod: none shown (open mode).
- What the stress-test draft found about the live town, unmeasured until the grant runs: one Fly Machine shared-cpu-2x / 2 GB, SQLite single writer, 13 agents, `/api/town` snapshot 26 KB in ~50 ms from a desk, 3 of 6 session slots in use. Ranked bottleneck candidates from the code: per-client WebSocket fanout on one thread, synchronous SQLite writes per tile step, the 2 GB Machine, Fly API polling per desk, Claude org limits (one killed a session on 2026-10-25).
- Spend to date (General pool): Cleo ~39.1 M tokens / ~$60 (blended ~$1.54/M); Dara 7.6 M / $4.46, stopped since 2026-10-22.

## Needs from Mitchell
1. Write the Prod key result in Prod → Settings → Key results. Suggested text from the town hall: "A stress test reports the max concurrent users/agents the live town supports and names the first two bottlenecks." The grant proposal then files itself at the next check (22:00 UTC) and lands in your Town Hall in-tray to fund, counter or reject.
2. Optional, when the proposal arrives: say whether the load ramps may run against production (announced windows, aborts after two degradations) or should run on a throwaway clone Machine first. The draft offers both.

## Reply from Mitchell (2026-10-26 15:45)

let's do load testing on a throwaway first, i don't want to break stuff that's running

