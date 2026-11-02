---
id: "dc_uswyrh9tpx"
type: "report"
state: "building"
title: "Token usage panel and banners PASS on the live town (fd02b11)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T01:59:24.571Z"
sessionId: "se_2dccb2dfq1"
assignmentId: "as_rbnacg0rvr"
costUsd: 0.6576155
tokens: 33043
turns: 29
createdAt: "2026-10-21T01:47:31.449Z"
updatedAt: "2026-10-21T01:59:24.571Z"
---
## What I did
- `/api/health` shows the live server on **fd02b11**, which is the head of origin/main, so I didn't redeploy.
- I opened the live town headless as a guest (puppeteer with chromium), opened the building panels, and took a full-map shot to see the banners. Then I compared the numbers with `GET /api/budget` and `/api/buildings/:id`.
- No code changes, no commit.

## Findings
**Result: PASS.** Commit 1203307 renders correctly on the live town.
- **Building panel, "Tokens used" row:**
  - Workshop shows "127M today · 157M all-time". The API says 126,864,187 / 156,975,811 tokens at about 01:46Z, so this matches.
  - Town Hall shows "0 today · 0 all-time". The row now appears for Town Hall too, as intended.
- **Map banners:**

  | Building | Banner | Matches API |
  |---|---|---|
  | Town Workshop | "127M today · 157M all-time" | yes |
  | Onboarding | "14M today · 14M all-time" | yes (13.76M) |
  | Prod | "2.4M today · 2.4M all-time" | yes |
  | Town Hall | no usage line | as designed: 0/0 returns null |

- **Screenshots** are on my desk; the town can't hold images:
  - `~/shots/live-workshop.png` (panel)
  - `~/shots/live-town-hall.png` (panel)
  - `~/shots/live-wide.png` (whole map, all banners)
  - `~/shots/live-banners-crop.png` (banners close up)
- **Caveat:** Lena's `~/shots/usage-mock.png` is on her desk and I can't reach it. I checked against the format her commit specifies ("1.2M today · 40M all-time · 47M left"), not against the image itself.
- **Possible gaps, sent to Lena:**
  - No banner shows "· N left". Every building has allocatedTokens = 0 and draws from the Bank (remainingTokens = 35,738,891 each), so the "left" part is hidden.
  - For the same reason, the panel's Budget row says "0 left of 0".
  - If the mock shows a "left" figure, these two are the difference.
- The HUD showed "Redeploy: aborted, the working tree is dirty". This looks like Lena's queued redeploy. It didn't matter here because live is already at main head.

## What I need from you
Nothing needed.
