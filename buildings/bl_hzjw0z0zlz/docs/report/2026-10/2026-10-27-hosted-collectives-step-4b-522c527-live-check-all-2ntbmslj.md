---
id: "dc_cy2ntbmslj"
type: "report"
state: "building"
title: "Hosted collectives step 4b: 522c527 live check, all 4 items pass (manual section seeded, HUD ? and slug work, README pointer live, hosted.count 0)"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "All 4 items pass live; nothing to assign. New manual hash 77d4684a… noted for the next manual edit (PAST_MANUAL_EDITIONS). Mitchell's checklist dc_kcjl97d3os stays the open human item; it goes in the next rollup."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-27T22:38:02.996Z"
sessionId: "se_7vqn062f9f"
assignmentId: "as_cih5s49igb"
costUsd: 0.4769719
tokens: 23849
turns: 15
createdAt: "2026-10-27T22:37:57.285Z"
updatedAt: "2026-10-27T22:38:02.996Z"
---
## What I did
I confirmed that health was 522c527 at 22:35Z. Then I checked the live manual over the API, drove the HUD "?" in headless Chromium (desk, 1280×900), fetched the GitHub README, and searched for a reply to [dc_kcjl97d3os](../../../../../town-hall/outbox/2026-10/2026-10-27-start-fund-and-retire-a-collective-with-a-second-g-jl97d3os.md). I changed no code, pushed nothing and did not redeploy (per Kelly's note).

## Findings
1. **PASS: live manual.** GET /api/manual returns doc [dc_irk1w62mpv](../../../../../library/article/2026-10/2026-10-27-operating-manual-k1w62mpv.md) (library), updated at 22:34:24Z by the boot seed. Its body is byte-identical to 522c527's docs/manual.md minus the h1 and has "## Start your own collective". The PAST_MANUAL_EDITIONS fix worked. The new live body hash is `77d4684ab7e1f1543c155ec41fac97dca585c5ae93b879d3a4c9aff0fbeb3e38`. Add it to PAST_MANUAL_EDITIONS before the next manual edit.
2. **PASS: HUD "?" and the section link.** On /workshop/, clicking `.help-btn` goes to `#/manual`, and the sheet contains "Start your own collective". The table of contents links `#/manual/start-your-own-collective`. Opening that URL directly scrolls to the H3 heading, which shows on screen. There were no console exceptions. Screenshots: /home/agent/shots/4b/live-help.png, live-slug.png.
3. **PASS: README.** GitHub main README.md line 23 is `### Start your own collective`. Line 25 is the hosted one-liner: "No server needed: you can also start a hosted collective at muster.town (Start a collective…, sign in with GitHub, bring an Anthropic API key)".
4. **PASS: Workshop and health.** /workshop/ returns 200 with the guest card and HUD intact. /api/health `hosted.count` = **0**.
- **Mitchell's checklist [dc_kcjl97d3os](../../../../../town-hall/outbox/2026-10/2026-10-27-start-fund-and-retire-a-collective-with-a-second-g-jl97d3os.md):** still open. There is no reply and no human-report yet, so the signed-in Start / fund / retire path is still unchecked.

## What I need from you
Mitchell: run the checklist in [dc_kcjl97d3os](../../../../../town-hall/outbox/2026-10/2026-10-27-start-fund-and-retire-a-collective-with-a-second-g-jl97d3os.md) with a second GitHub account and reply with any box that fails.
