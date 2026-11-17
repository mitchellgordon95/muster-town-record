---
id: "dc_a9ou7acgvg"
type: "report"
state: "building"
title: "Proposed gr_ptle4vvujl: get homepage visitors into a working town"
authorId: "ag_3p26r0njfe"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Proposal gr_ptle4vvujl stands; rendered its money ask for Mitchell. Nothing to queue until he funds it."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-17T03:30:32.453Z"
sessionId: "se_vkjcc7ew5c"
assignmentId: "as_pectnnbm4j"
costUsd: 1.3956979999999999
tokens: 69785
turns: 31
createdAt: "2026-11-17T03:29:14.955Z"
updatedAt: "2026-11-17T03:30:32.453Z"
---
## What I did
Read the live join funnel, looked at muster.town/ in headless chromium at 1400x900 and 390x844, read the homepage card and Start-a-collective code, wrote findings [dc_i431k2hvpy](../../note/2026-11/2026-11-17-findings-most-homepage-visitors-never-enter-a-coll-31k2hvpy.md), and proposed gr_ptle4vvujl (400,000 tokens, 4 steps M+S+M+S) under ob_508f35a2m4.

## Findings
- The first funnel step loses the most people. From 11-11 to 11-16 there were 61 homepage views and 13 guest visitors across both towns (Workshop 10, Trauma 3), about 21%. Over 30 days: 319 home views, 85 guest visitors, 6 sign-ins started, 2 signed in (GET /api/join-funnel).
- A first visit to muster.town opens a three-page pitch card over the tiles. The only route into a town from the card is "Open Workshop Collective" on page 3. On a phone the card covers the whole screen. Inside a town a second first-visit card appears.
- We can't see where visitors leave: nothing counts card pages, Skip/×, Open or tile clicks. isAutomatedClient doesn't drop Googlebot or bingbot, so some home views may be crawlers. The 21% figure is a proxy, roughly 10–35%.
- The plan is to measure first, then fix the one leak the counts point to. It stops after step 2 if the card turns out not to be the leak. KRs: kr_9me8p8vsds, kr_vs328w3bkh, kr_zqoqkyrk7z.
- Risk: deploys are stuck at 5974c42b (FYI [dc_4yrb3979ty](../../../../town-hall/docs/fyi/2026-11/2026-11-16-nothing-merged-since-18-52z-is-live-ci-s-deploy-to-rb3979ty.md)), so step 1 can't be checked live until that is fixed.

## What I need from you
Fund, counter or reject gr_ptle4vvujl in the Town Hall decision queue.
