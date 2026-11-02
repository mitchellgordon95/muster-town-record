---
id: "dc_8ce0993ntq"
type: "report"
state: "building"
title: "Exploration: the Bank answers only in tokens, and hosted collectives show the hub's machine as their own cost; proposed gr_gmzli3f96j (300k)"
authorId: "ag_k1uj95h1v0"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_gd8yuqk7t9","dc_rke20gvrqr","dc_i2ln43k253"],"urls":["https://muster.town/api/finance","https://muster.town/hollyville/api/finance/fly"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Clean exploration: findings dc_gd8yuqk7t9 and proposal gr_gmzli3f96j filed. The decision it asks for (dollars on the Bank, or only key result 3) is Mitchell's and reaches him through the proposal in the Town Hall in-tray, so no rollup Needs line and no new assignment. The Hosting-tab double count (routes/town.ts passing !!FLY_APP_NAME for every World) stays inside the proposal rather than starting as exploration, to avoid duplicating a pending plan."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-01T01:17:14.311Z"
sessionId: "se_5kl6lxmq2n"
assignmentId: "as_i39qesuqxq"
costUsd: 1.0770039000000002
tokens: 53850
turns: 22
createdAt: "2026-11-01T01:16:44.377Z"
updatedAt: "2026-11-01T01:17:14.311Z"
---
## What I did
Read live finance endpoints for the Workshop and Hollyville (signed out, live c1cdd23, 2026-11-01 01:15Z) and the code on main 7521c0b. Skipped the adjusted-token mix idea because directed schedule sc_p5oj6u7pks already covers it and PR #231 changed the unit. Wrote findings [dc_gd8yuqk7t9](../../note/2026-11/2026-11-01-findings-the-bank-shows-tokens-but-no-dollars-and-8yuqk7t9.md) and proposed gr_gmzli3f96j.

## Findings
- **No dollars on the Bank.** /api/finance, /spend and /sources return tokens only (used 75,848,871; burn 9,573,638 a day). Since PR #231 (Opus 5.5 unit, $20 per million output tokens), a new token has a fixed list-price dollar value, so adding dollars is now cheap. Past totals have to be priced per session, though: before migration 076, Fable usage was booked in Fable output tokens, so multiplying everything by $20 would read it 2.5× low.
- **Hosted collectives count the hub's machine as their own cost.** GET /hollyville/api/finance/fly shows $31.96 of Town Machine over 30 days, with a window that starts on 2026-10-03, before the collective existed. The cause is that server routes/town.ts:380 passes `!!FLY_APP_NAME` for every World. The Workshop shows the same dollars, so the hub's machine is counted twice.
- The /api/finance/pools 404 is expected, since pools were deleted in PR #169.
- Proposal gr_gmzli3f96j has three key results, all due 2026-11-07:
  - Overview rows show "≈ $X at API list price".
  - Spending rows show dollars, with a ✓ line that checks them.
  - The hosted Hosting tab says muster.town runs the server.
  It is display only (no charge, no migration), and the ask is 300,000 tokens.

## What I need from you
Decide on gr_gmzli3f96j, including whether list-price dollars belong on the Workshop's subscription-funded Bank page (or fund only key result 3).
