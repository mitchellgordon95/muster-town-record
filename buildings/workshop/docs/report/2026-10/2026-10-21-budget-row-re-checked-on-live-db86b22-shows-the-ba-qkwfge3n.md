---
id: "dc_5xqkwfge3n"
type: "report"
state: "building"
title: "Budget row re-checked on live db86b22: shows the Bank share left, correct"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T03:58:23.312Z"
sessionId: "se_l452jija1h"
assignmentId: "as_8v2b98tj9p"
costUsd: 0.1877102
tokens: 9471
turns: 11
createdAt: "2026-10-21T03:58:05.630Z"
updatedAt: "2026-10-21T03:58:23.312Z"
---
## What I did
I checked the Budget row fix (57230b8) again in a browser. This time I used the newest live build, db86b22. 57230b8 is an ancestor of that build. I used headless Chromium as a guest and opened the Town Workshop building panel on its Overview tab. I made no code changes, so I didn't commit or redeploy.

## Findings
- The panel's Budget row reads **"18M left to draw from the Bank"**. It no longer says "0 left of 0".
- That matches the API: `/api/buildings/workshop` returns `bankTokens` = `remainingTokens` = 17,695,185 tokens, which the panel rounds to 18M. It was 29M at my last check, so it is going down as tokens get spent.
- Other rows on the panel: Tokens used 143M today · 173M all-time, Spent $78.01.
- There were no page errors. Screenshot: ~/shots/live-budget2.png on my desk.
- I had already confirmed this fix live in [dc_04pj27ghbr](2026-10-21-live-check-passed-budget-row-and-building-sign-now-pj27ghbr.md), so this assignment repeated that check. It's done.

## What I need from you
Nothing needed.
