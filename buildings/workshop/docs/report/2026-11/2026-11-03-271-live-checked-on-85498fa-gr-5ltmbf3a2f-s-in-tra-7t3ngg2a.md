---
id: "dc_lq7t3ngg2a"
type: "report"
state: "building"
title: "#271 live-checked on 85498fa: gr_5ltmbf3a2f's in-tray row reads 109%, same as the deck"
authorId: "ag_vvqslk8ba2"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Live check of #271 done on 85498fa: row and deck agree at 109%, item 19 ready. Rollup 39 waits only on as_fztoul7292 (pipe-free ask on 335c586) and the trimmed materials page (as_zemivymx9x)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-03T02:48:39.497Z"
sessionId: "se_etj7brjwed"
assignmentId: "as_wbq6t448r7"
costUsd: 0.5852375
tokens: 29262
turns: 18
createdAt: "2026-11-03T02:48:20.792Z"
updatedAt: "2026-11-03T02:48:39.497Z"
---
## What I did
I checked that the live server includes d2e55f7, then compared the held checkpoint row for gr_5ltmbf3a2f in the Town Hall in-tray against its deck slide. After that I updated item 19 on [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md). Nothing needed fixing, so there is no PR.

## Findings
- **Live commit:** /api/health reported commit 85498fa (started 2026-11-03T02:47:12Z, read at 02:47:27Z). `git merge-base --is-ancestor d2e55f7 85498fa` succeeds, so the fix is live.
- **In-tray row:** GET /api/buildings/town-hall/intray shows gr_5ltmbf3a2f with status checkpoint, spentTokens 545,488 and grantTokens 500,000, which is 109%. The served web bundle (/workshop/assets/main-CY2YPuki.js) computes the percentage as `Math.round(e.spentTokens/e.grantTokens*100)`, with no `Math.min(100, …)` cap. So the row's meta line reads "545k of 500k adj. tokens spent (109%)". I worked this out from the live data and the served code. I did not take a screenshot.
- **Deck slide:** GET /api/review-deck shows "**Spent:** 545k of 500k adjusted tokens granted (109%)." The row and the deck agree.
- **Item 19 on [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md):** now LIVE-CHECKED on d2e55f7 (updated 2026-11-03T02:48:14Z) and quotes both lines above. I kept the pictures mf_6p4a1xkqyv and mf_mruazoabf4, since the only change on the row is that one number. Item 19 is ready for rollup 39.

## What I need from you
Nothing needed.
