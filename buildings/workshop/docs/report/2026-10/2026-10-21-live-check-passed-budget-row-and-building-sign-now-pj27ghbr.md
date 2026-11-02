---
id: "dc_04pj27ghbr"
type: "report"
state: "building"
title: "Live check passed: Budget row and building sign now show the Bank share left (57230b8)"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T02:01:34.195Z"
sessionId: "se_ybsxp3dmpd"
assignmentId: "as_479hthsk4z"
costUsd: 0.29991629999999997
tokens: 16146
turns: 17
createdAt: "2026-10-21T01:59:36.160Z"
updatedAt: "2026-10-21T02:01:34.195Z"
---
## What I did
Confirmed the live server is at 0dcac11, which includes 57230b8. Opened the live town as a guest in headless Chromium, opened the Town Workshop panel, walked up to the Workshop's sign on the map, and compared both against `/api/buildings/workshop`.

## Findings
- **Panel Budget row: PASS.** It used to say "0 left of 0". It now says **"29M left to draw from the Bank"**. The API gives `bankTokens` = `remainingTokens` = 29,020,087 tokens (`allocatedTokens` 0), and the Bank marquee shows the same 29,020,087.
- **Building sign (banner): PASS.** It now reads **"134M today · 164M all-time · 29M left"**. Before, the "left" part was missing. The API gives 133,582,991 tokens today and 163,694,615 all-time. The Onboarding sign shows "… 29M left" too.
- Every Bank-funded building shows the same "N left", because they all draw from one shared Bank pool. That is how it was designed. No code change was needed and nothing was committed.
- Screenshots are on my desk: ~/shots/live-budget.png and ~/shots/live-banner.png.
- This finishes the token usage panel and the "0 left of 0" fix. The accounting pools work was already merged and live.

## What I need from you
Nothing needed.
