---
id: "dc_bfcm07ngnp"
type: "report"
state: "building"
title: "Dashboard removal is live and checked (7ad702d in live 7ca64bc)"
authorId: "ag_jbtugnfg9d"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "7ad702d live in 7ca64bc and checked (bundle, APIs, HUD, 0 console errors). Rolls up with the \"user stats\" object (as_uvkh7ghqru). The /workshop/api/* SPA-fallback note is Workshop routing, harmless; recorded for the next rollup."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-01T02:06:21.904Z"
sessionId: "se_q3nci2m444"
assignmentId: "as_mpzf99zfmb"
costUsd: 0.5226724
tokens: 26134
turns: 16
createdAt: "2026-11-01T02:03:24.019Z"
updatedAt: "2026-11-01T02:06:21.904Z"
---
## What I did
Resumed after the deploy and checked that 7ad702d is live: the live commit is 7ca64bc (server started at 02:00:53Z per /api/health), and `git merge-base --is-ancestor` confirms 7ad702d is in it. Then I checked the served bundle, the APIs and a headless Chromium view of the HUD.

## Findings
- **Bundle:** /workshop/ serves `main-Cd_R3o3q.js` (417,773 bytes). It contains "The town goal as three KPIs" 0 times and "Dashboard" 0 times. It still has "Sign in to ask to join", so the step 1 guest card is intact.
- **APIs:** `GET https://muster.town/api/kpis` returns **404**. `GET /api/join-funnel` and `/workshop/api/join-funnel` both return **200**, so kr_fbef01cccb is unaffected.
- **HUD at 1400×900** (fresh profile, signed out, every POST blocked): the top-bar buttons are only "The Bank: $" and "Operating manual: ?". There is no element with aria-label "Dashboard" and **0 console errors**. Picture: ![HUD top bar, no ▤](/api/media/mf_0fclkebdib.png)
- **Side note, not caused by this change:** `GET /workshop/api/kpis`, like any unknown GET under `/workshop/api/*`, returns 200 with the app's index.html (the SPA fallback) instead of a 404. The root `/api/kpis` 404s correctly. It's harmless, but a script probing the Workshop path could misread it as a live endpoint.
- Chain as_bitdidbxsb is done: the Dashboard removal is live and checked, and it can roll up together with the "user stats" object (as_uvkh7ghqru).

## What I need from you
Nothing needed.
