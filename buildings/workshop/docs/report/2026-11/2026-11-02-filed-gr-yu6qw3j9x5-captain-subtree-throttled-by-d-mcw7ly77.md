---
id: "dc_9tmcw7ly77"
type: "report"
state: "building"
title: "Filed gr_yu6qw3j9x5: captain subtree throttled by desks + min exploration cap (replaces rejected gr_kph1zjjrzg)"
authorId: "ag_w5k62ad2zs"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Proposal gr_yu6qw3j9x5 filed per 1:1 mt_a6wb51enia D3; the brief now shows it funded (500,000), so its first step comes as its own \"Grant funded\" assignment."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-02T03:29:57.712Z"
sessionId: "se_q394ef253k"
assignmentId: "as_u9e1x19y3o"
costUsd: 0.6029533
tokens: 30148
turns: 16
createdAt: "2026-11-02T03:29:11.014Z"
updatedAt: "2026-11-02T03:29:57.712Z"
---
## What I did
Read the code at main 024b236 (explore.ts, free-tokens.ts, the building desk routes) and filed one grant proposal, **gr_yu6qw3j9x5** (goal gl_join, 250,000 tokens, findings [dc_7yr1fea9lc](../../note/2026-11/2026-11-02-findings-a-non-admin-captain-can-commit-the-shared-r1fea9lc.md)). The notes for mt_a6wb51enia aren't filed yet, so they aren't linked. I built nothing.

## Findings
- **KR1 kr_h0pqsgkov8 (due 11-05):** the explore assignment text (core explore.ts l.70) must name docs/how-work-gets-done.md §7 (Bank, free tokens) and §8 (caps) as required reading. A core test checks this.
- **KR2 kr_86wt7nnrfg (due 11-06):** `exploreCapAt` (free-tokens.ts l.21) uses the nearest cap today. It will use the smallest cap on the path and keep the same return shape. Tests: root 500,000 with child 5,000,000 → 500,000; child 100,000 → 100,000. The goal detail shows which goal's cap applies.
- **KR3 kr_jya7n4g88a (due 11-08):** a building's desk count is its `headcount`, which only admins can change today (ops.ts updateBuilding l.57, needs town.manage_buildings). The plan adds one nullable column, `goals.desksTotal` (migration 083; the highest on main is 082).
  - Who sets it: the captain above or an admin. The goal's own captain can't.
  - What it blocks: any change that adds desks to the subtree (raising headcount, a new building, attaching a building) returns 409 naming the goal and its total.
  - **Admins are gated too.** Only admins can change desks today, so exempting them would make the gate do nothing. The note asks Mitchell to counter if he wants admins exempt.
  - Display: the goal panel shows "Desks: N of M".
- **Stop condition:** stop and report if the desk gate needs any schema change beyond that one column.
- **Note for Mitchell (in the proposal):** the per-captain budget KR is dropped on his word. The min-cap rule stays because today a captain can loosen the cap set above them.
- **Why 250,000:** step 1 of gr_zsm1piyqyx used about 200,000 with no migration. This grant has 3 changes, a migration, a web line and 1–2 rounds of CI and redeploy.
- **Still open:** D1 also said to withdraw gr_kph1zjjrzg, but Mitchell already rejected it, so as_r8wz26kata's withdraw step for it can be dropped.

## What I need from you
Nothing needed.
