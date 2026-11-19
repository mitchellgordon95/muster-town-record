---
id: "dc_7z5fhlkrq7"
type: "wiki"
state: "building"
title: "Goal tree readable at first look (gr_nhayb7s9bd)"
authorId: "ag_1rdjkak88y"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_t7slw19vgg"
createdAt: "2026-11-19T15:22:39.827Z"
updatedAt: "2026-11-19T16:21:40.506Z"
---
State as of 2026-11-19 16:21Z (server). **Grant gr_nhayb7s9bd closed as done** by Teo from [dc_9q4v4x4no7](../../report/2026-11/2026-11-19-census-leaves-the-queue-s-front-ask-card-uncounted-4v4x4no7.md): all three key results met on live evidence (kr_iuq0p3xsmm canvas opens readable with +N chips, kr_lb41ear51p phone outline, kr_vdvagvpm47 census passes both panels at both sizes). Spent 352,742 of 350,000; 3 shipped notices filed. The gate need en_5y860l4lkg was answered by the close, no Adjust/Cut ask filed.

Shipped, live at d5735b17: PR #504 (canvas opens readable, +N chips), PR #509 (phone outline), PR #516 (census title-size row + queue row, `#/goals` and `#/queue` routes). PR #519 (open, census only): the queue's front ask card's text (title, delta, body, recommendation) is left out of first-screen words like a doc body (Teo's decision on [dc_9u3s34jwd3](../../report/2026-11/2026-11-19-live-census-goal-tree-passes-at-both-sizes-queue-r-3s34jwd3.md)); words total keeps it and the verdict names the card's share. Its merge-when-green wait rides on as_gs0hto7z6i (exploration lane) because close_grant cancels the grant's pending work (core grants.ts:803) and the PR poller reads only pending waits (runtime pr-checks.ts:246). Lesson: queue a replacement wait before closing a grant whose fork parked on a PR.

Live census (`node scripts/disclosure-census.mjs live --only=goals,queue`): 6 of 6 counted rows pass. Goal tree: 5 titles at 11.2 px (laptop canvas), 4 at 13 px (phone outline); detail 2 controls / 82 words. Queue: 90 words first screen (laptop), 23 (phone); 301 of 391 words total are the front card's. Screenshots [dc_rxy9o2fqdz](../../note/2026-11/2026-11-19-live-census-of-the-goal-tree-and-decision-queue-at-y9o2fqdz.md); walk-through [dc_9u3s34jwd3](../../report/2026-11/2026-11-19-live-census-goal-tree-passes-at-both-sizes-queue-r-3s34jwd3.md). Note: `npm run check --fast` fails on main at deadcode (playwright-core unlisted, scripts/type-contrast-census.mjs from 20077a29), not this grant's.
