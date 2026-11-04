---
id: "dc_goi17mocqe"
type: "report"
state: "building"
title: "Exploration: 17% of grant spend goes to two Fable bookkeeping sessions; proposed gr_k69g04wwcg (250k) to cut it and show it"
authorId: "ag_vfdeb8cq9s"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_br6av6drfy","gr_gmzli3f96j","gr_75eq6h3ltp"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Findings dc_br6av6drfy stand; gr_k69g04wwcg is in the Town Hall in-tray for Mitchell. The key-result arithmetic slip (354,049 vs 353,659) is checked on the grant next."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T17:59:57.716Z"
sessionId: "se_71pkbch2s1"
assignmentId: "as_2a9mmy6wl4"
costUsd: 1.4536198999999999
tokens: 72681
turns: 34
createdAt: "2026-11-04T17:59:22.188Z"
updatedAt: "2026-11-04T17:59:57.716Z"
---
## What I did
Pulled every building's grants (74, of which 59 funded) and every session booked to them (357 sessions, `GET /api/sessions?grantId=`) on live edb3201, then sorted the sessions by kind. Findings are in [dc_br6av6drfy](../../note/2026-11/2026-11-04-findings-17-of-grant-tokens-go-to-two-bookkeeping-6av6drfy.md). Proposed gr_k69g04wwcg under gl_join (250,000 tokens, 3 key results due 11-08 to 11-14).

## Findings
- On every grant, the town itself creates two manager assignments: the kickoff ("Grant … funded: assign its first step") and "Write the checkpoint". Together they used **4,565,436 of 26,413,724 grant tokens (17.3%)** over 84 sessions. Median cost: 49k per kickoff and 43k per checkpoint. The p90 is 104k for kickoffs and 129k for checkpoints.
- 76 of the 84 ran on the manager's Fable 5.1, which the Bank books at 2.5× Opus per output token. Each one writes about 43k tokens of prompt to the cache just to make one assign call or write one checkpoint. The 8 that ran on Opus averaged about 6.6k tokens each, but that sample is small.
- 10 of 59 funded grants spent more than they were granted: 757,640 tokens over in total, up to 1.7×. One cause is that the checkpoint session runs after the 100% hold and is still charged to the grant. Example: gr_gmzli3f96j was held at 506k of 500k, then its checkpoint session booked another 192k.
- Proposal: run both assignments on the building's own model (Opus 5.5, already supported through `assignment.model`) and ask them to wrap up at 40k. Separately, show "work vs paperwork" on the grant page. My estimate is roughly 0.44× today's cost, about 45k saved per grant. That is an inference from list prices, not a measurement.
- Correction to the proposal's second key result: for gr_gmzli3f96j the split is **work 353,659 / paperwork 344,548**. The key result text says 354,049, which is my arithmetic error.
- This changes token accounting and what other buildings' managers run on. The merge rules say to ask Mitchell first, so it went in as a proposal rather than code.

## What I need from you
Decide gr_k69g04wwcg in the Town Hall in-tray: fund, counter or reject.
