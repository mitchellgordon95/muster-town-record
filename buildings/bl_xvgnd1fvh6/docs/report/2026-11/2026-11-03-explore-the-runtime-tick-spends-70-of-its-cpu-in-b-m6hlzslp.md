---
id: "dc_unm6hlzslp"
type: "report"
state: "building"
title: "Explore: the runtime tick spends ~70% of its CPU in Bank.expectedSession; proposed gr_db6ofyd0yf (160k) to halve it"
authorId: "ag_283aw19yjp"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_avj0n0doki","dc_er6dxw6kil","dc_ur1qzaxafp"],"urls":["https://muster.town/api/health"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Exploration done: tick CPU profiled (Bank.expectedSession ~70% of tickOnce), proposal gr_db6ofyd0yf (160k, Bank code for speed only) is in the Town Hall in-tray and reaches Mitchell on its own. Nothing runs until he funds it; a funded decision wakes me with the first-step assignment."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-03T02:54:25.376Z"
sessionId: "se_7o817ou0jj"
assignmentId: "as_kq9l586x64"
costUsd: 0.8685415
tokens: 43427
turns: 18
createdAt: "2026-11-03T02:54:11.803Z"
updatedAt: "2026-11-03T02:54:25.376Z"
---
## What I did
- Sampled /api/health 14 times (02:50–02:52Z 11-03).
- Re-ran the step-1 tick benchmark at 1× world on main 335c586 under a CPU profiler.
- Checked open PRs and docs: nobody is working on the tick cost. gr_n0p3ast5pp covers docs and the WebSocket broadcast, not the tick.
- Filed the findings ([dc_avj0n0doki](../../note/2026-11/2026-11-03-explore-the-runtime-tick-spends-70-of-its-time-rec-j0n0doki.md)), the topic page "Runtime tick cost" ([dc_ur1qzaxafp](../../wiki/2026-11/2026-11-03-runtime-tick-cost-gr-db6ofyd0yf-1qzaxafp.md)) and the proposal gr_db6ofyd0yf.

## Findings
- **Live tick:** median ≈ 199 ms (range 183–220). Phases: work 90–110, explore 39–47, streams 29–36 ms. The slowest tick after boot was 856 ms. lagMs spiked to 170 ms once in the 14 samples.
- **Desk at 1×:** tick p50 132 ms, p95 185 ms.
  - **Bank.expectedSession is about 70% of tickOnce CPU** (3.2 s of 4.4 s). It reloads every work session from the last 7 days as full rows on every tick and on every session start.
  - Next costs: Bank.debited/available at 1.7 s and 1.5 s inclusive (one debit sum per credit per candidate), then freeTokensAll inside exploreTick at 0.85 s.
- **Expected effect** of memoizing expectedSession, summing debits once and making one freeTokensAll call per exploreTick: desk 1× tick about 130 → 50 ms, live about 200 → 100 ms (±30%). The 500 ms crossing would move from about 1.5× toward about 3× the live world, which the bench re-run checks.
- **Proposal gr_db6ofyd0yf**, 160k tokens, on goal gl_65fywzdb9y:
  - **KRs:** live tick median under 110 ms with streams under 10 ms; desk p95 ≤ 250 ms at 2× and ≤ 900 ms at 4× in docs/scaling.md; tests pin that no Bank number changes.
  - **Stop condition:** stop if step 1 saves less than 30%.

## What I need from you
Decide on gr_db6ofyd0yf in the Town Hall in-tray. It changes Bank code (bank.ts, budget.ts) for speed only, so under the merge rule funding it is your yes.
