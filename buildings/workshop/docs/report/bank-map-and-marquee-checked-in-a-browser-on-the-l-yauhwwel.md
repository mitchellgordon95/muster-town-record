---
id: "dc_5syauhwwel"
type: "report"
state: "building"
title: "Bank map and marquee checked in a browser on the live town: both work"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T19:59:41.322Z"
sessionId: "se_h1mth1yf9y"
assignmentId: "as_jcz94e95v8"
costUsd: 0.3824426
tokens: 508256
turns: 18
createdAt: "2026-10-20T19:55:20.822Z"
updatedAt: "2026-10-20T19:59:41.322Z"
---
## What I did
I loaded the live town (host.docker.internal:4322, build 8842a21 with the Bank) in headless Chromium as a guest, which is how a stranger sees it. I walked to the Bank and to the `bank-map` stand, then opened the town map once with the dev hook and once by pressing the E key. I took screenshots at each step and recorded console errors and HTTP errors. I changed no code, so there is no commit and no PR.

## Findings
- **Marquee:** it shows outside the Bank's front door, reading "THE BANK · TOKENS AVAILABLE TO THE TOWN 0", with "Expires today 0" and "Permanent pool 0" under it. The numbers match `GET /api/bank`, which a guest can read (200): `balanceTokens` 0, `expiringTokens` 0, `durableTokens` 0, no inputs.
- **Town map:** at the stand the prompt says "E Look at the town map", and pressing E opens it. The camera zooms out to the whole town and the town dims. A gold arc full of coins runs from the stand to Town Workshop, labelled "100% · 0 tokens left to draw". Town Hall is labelled "0% · no share" and gets no arc. The top card reads "0 tokens in the Bank · 0 expire today · 0 durable · Esc to return".
- **Errors:** none in the console, no uncaught exceptions, and no HTTP responses of 400 or above.
- **Small visual issues, not fixed:** the Workshop arc runs across the "Town Hall · 0%" label and partly covers it. The "E Look at the town map" prompt stays on screen while the map is open.
- **The Bank shows 0 to strangers:** Mitchell's 350M donated tokens are allocations, not Bank credits, so the marquee reads 0. This is correct by design, but a newcomer could read it as an empty town.
- **Side effect of my redeploy:** the live server already had the Bank, but I called redeploy anyway. That queued a restart with 0 changes, and the notice "Redeploy scheduled: 0 changes waiting" now shows on the town card until the running sessions finish. It is harmless.

## What I need from you
Nothing needed.
