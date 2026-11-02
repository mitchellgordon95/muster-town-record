---
id: "dc_x53ragnl6j"
type: "report"
state: "building"
title: "6105e18 verified live: the Bank books in adjusted output tokens; grant and subscription figures converted at 30:1"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Bank step 3 verified live: accounting \"adjusted\", booked = adjusted exactly on two post-deploy sessions, conversion audited in event 24344. The ask to confirm the converted figures goes to Mitchell in rollup 14 (already in rollup 13)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T00:38:32.791Z"
sessionId: "se_sk2d8i5uio"
assignmentId: "as_v2cni1duim"
costUsd: 0.5055000000000001
tokens: 20994
turns: 15
createdAt: "2026-10-27T00:37:30.807Z"
updatedAt: "2026-10-27T00:38:32.791Z"
---
## What I did
Checked the live server. 6105e18 is part of the live commit (a5026c3). I checked `/api/health`, the `bank.converted` event, `/api/bank` inputs, the grant's spent figure and the charges for the sessions since the deploy.

## Findings
- **/api/health** shows `accounting: "adjusted"`. That is the check for kr_vyrhhiyotb.
- **Conversion audit:** event 24344 (`bank.converted`, 2026-10-27 00:00) records every figure before and after at 30 raw (Opus) / 24 raw (Fable) per adjusted token.
- **gr_iq5m7dug56:** the ask went from 24,000,000 to **800,000 adj.** as planned. Mitchell's later raise to 50,000,000 raw became **1,666,667 adj.** Its spent figure is now 1,619,043 / 1,666,667 adj. (`grants.ts` adds up each session's adjustedOutputTokens).
- **Subscription inputs:** bi_au5kt05vlj went from 40,000,000 to **1,333,333 adj./day** (weekly cap 9,333,333). bi_foh0utko9b went from 20,000,000 to **666,667 adj./day** (weekly cap 3,333,333). Each input still shows the five counters alongside, e.g. bi_au5kt05vlj credited 5,656,566 output + 234,343,434 cache read = 8,000,000 adj.
- **Booked = adjusted:** the two sessions finished after the deploy match exactly (0% difference):
  - se_l8yww7dhbh: 228,898 raw, adjustedOutputTokens 7,630, booked 7,630
  - se_tzmp1wnr1l: 201,287 raw, 6,709 adjusted, booked 6,709

  That is inside the 10% target.
- Bank step 3 is done and live.

## What I need from you
Mitchell: please confirm the converted figures in the new unit: 1,333,333 and 666,667 adj./day for the two subscription inputs, and 1,666,667 adj. for gr_iq5m7dug56.
