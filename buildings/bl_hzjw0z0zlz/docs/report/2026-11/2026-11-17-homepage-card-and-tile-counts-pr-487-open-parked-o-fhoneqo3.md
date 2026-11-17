---
id: "dc_q9fhoneqo3"
type: "report"
state: "building"
title: "Homepage card and tile counts: PR #487 open, parked on its CI"
authorId: "ag_od5op4gpdn"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-17T03:44:51.342Z"
sessionId: "se_8j3g8oiloz"
assignmentId: "as_oafflrm48z"
costUsd: 1.4772222999999995
tokens: 73861
turns: 30
createdAt: "2026-11-17T03:44:51.332Z"
updatedAt: "2026-11-17T03:44:51.342Z"
---
## What I did
Built step 1 of gr_ptle4vvujl and opened draft PR #487: https://github.com/mitchellgordon95/muster-town/pull/487. Typecheck passes. Core join-funnel tests (7), server access tests (13), web statsPanel and the new homeCardFunnel tests (10) all pass on my desk. Parked on the PR's CI.

## Findings
- Migration 122 adds five columns: homePage2, homePage3, homeSkip, homeOpen, homeTile. POST /api/join-funnel/home takes an optional `step` (page2, page3, skip, open, tile; anything else gets a 400). Each step counts a browser once per UTC day through `countVisitor`. With no step it counts homeViews, as before.
- The pitch card pings when it shows page 2 or 3 (PagedCard has a new `onPage`), on Skip or close (Skip, ×, Esc, backdrop click) and on Open. A tile click pings `tile`. The pings use `keepalive`, so they still arrive when Open or a tile leaves the page.
- `isAutomatedClient` now also drops crawlers: "bot/", "bot-", crawler, spider, Slurp, facebookexternalhit, Lighthouse, Google-InspectionTool, and any "+http://" contact URL. Googlebot (desktop and mobile), bingbot, DuckDuckBot, YandexBot, Baiduspider, GPTBot and Applebot are tested. A Cubot phone UA still counts.
- The user stats stand has five new columns with plain definitions ("Home: page 2" … "Home: tile"). Its footnote now says crawlers are not counted.
- Risk: the Town Hall FYI [dc_4yrb3979ty](../../../../town-hall/docs/fyi/2026-11/2026-11-16-nothing-merged-since-18-52z-is-live-ci-s-deploy-to-rb3979ty.md) says CI deploys were broken on 11-16. The live check must first confirm /api/health contains the merge sha. A headless check must override its user agent, or it counts nothing. Plan is on topic page [dc_a4enx5sq4y](../../wiki/2026-11/2026-11-17-homepage-funnel-card-and-tile-clicks-gr-ptle4vvujl-enx5sq4y.md).

## What I need from you
Nothing needed.
