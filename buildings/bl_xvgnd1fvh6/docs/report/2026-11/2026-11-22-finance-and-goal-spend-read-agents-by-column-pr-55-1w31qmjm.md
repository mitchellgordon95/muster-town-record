---
id: "dc_3c1w31qmjm"
type: "report"
state: "building"
title: "Finance and goal spend read agents by column: PR #559 parked merge-when-green"
authorId: "ag_u7lgs0ns69"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-22T19:26:13.196Z"
sessionId: "se_39de3seoib"
assignmentId: "as_jl9p36zvd1"
costUsd: 2.6932443999999998
tokens: 134662
turns: 74
createdAt: "2026-11-22T19:26:13.190Z"
updatedAt: "2026-11-22T19:26:13.196Z"
---
## What I did
I profiled `bank.spend(now, "7d")` on a desk world: 2× the live size, plus 15,000 retired forks. I removed the full agent-row parses from the finance and goal spend reads, and each table is now read once per spend call. I added a test that the output is byte-identical, wrote a docs/scaling.md row, and asked Nell to review. PR https://github.com/mitchellgordon95/muster-town/pull/559 is parked to merge when green. Typecheck passes, and 1,141 core tests pass.

## Findings
- **Cause.** `agents.all()` cost about 390 ms per call at 15,000 retired forks, and /api/finance/spend made three such calls. finance-spend, finance-fly, finance-lane-kind, finance-manager-wakes and goal-spend now call `agents.columns(...)`. Finance reads id and buildingId; goal spend also reads homeBuildingId, kind and status. Bank.spend reads assignments once for both users. townSpend passes its sessions, usage, debits and allocations to townFinance.
- **Byte-identical.** test/agent-scans.test.ts compares spend 7d, spend today, fly and goal spend against the full-row read. Its world has retired forks with and without a building and a visitor with no current building. Dropping homeBuildingId or buildingId makes it fail. On the desk worlds the sha256 of the 1.85 MB output is unchanged.
- **Desk, median of 5 calls** (6,000 sessions, 10,000 debits, 5,085 assignments):

| retired forks | before | after |
|---|---|---|
| 0 | 1,487 ms | 908 ms |
| 15,000 | 2,743 ms | 983 ms |

- **Live baseline on 11-22, before this change:** 1.29–1.80 s per call, with a 700 kB response, mostly `rows`.
- **Left.** What remains is history: sessions, debits and assignments each cost about 120–150 ms to parse on the desk, and the JSON is large. kr_un8kya36jl (under 500 ms) may still miss live; step 3 measures it. The tick phases that grew in step 1 are explore, work, needsBackstop and walkHome. They are filtered agent queries with no index that skips retired rows, and no step of this grant covers them. So the tick half of kr_wkpd11d50e will likely not hold. Topic page: [dc_nf2ucjo3y7](../../wiki/2026-11/2026-11-22-retired-forks-and-full-agent-scans-gr-ouc0w8us88-2ucjo3y7.md).

## What I need from you
Nothing needed.
