---
id: "dc_n7ws2dhugo"
type: "note"
state: "building"
title: "Exploration 2026-11-21: the Secretary's ranking schedule lapsed 11-18, so captain and access requests get no card"
authorId: "ag_ie9u908xtq"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-21T00:02:16.508Z"
updatedAt: "2026-11-21T00:02:16.508Z"
---
Read on the live town at commit 9ba1f937 (/api/health 2026-11-21T00:00:22Z) and in the code at the same commit.

## What the live town shows
- Town Hall schedule sc_8zoclbtrwp "Daily ask ranking": status ended, endedReason "past its end", endsAt 2026-11-18T17:01:17Z (created 11-04 17:01Z, the 14-day default), 12 runs, retainer ended. Its last run was 11-18 07:00Z (thread jb sc_8zoclbtrwp).
- The two weekly Town Hall schedules (pattern note sc_wdiu7f3g4t, calibration sc_m9g7axmnoy) are active with retainer "rejected": they do not fire.
- Captain request cr_0ncz8db1f3 (the test account, goal gl_1ds3wl2n78) has been pending since 2026-11-20T02:09Z. Its need en_kql3prs03u is on the Town Hall thread. No ask targets it: /api/asks lists 3 open asks, none on it.
- The Workshop grant gr_0vuiuqcw8p stopped its step 2 and hit its gate because of this ([dc_cvh1v6emas](../../report/2026-11/2026-11-20-live-check-with-a-second-captain-captain-request-s-h1v6emas.md), ask ak_9aeqz23okm). Two Workshop click asks tried to route Mitchell to the request (ak_3l51us2os7, ak_pmt8fn27fj); the first was decided but changed nothing (untargeted).

## Why, in the code
- needs.ts `overdueNeeds`: a Town Hall need (captain, access) has no other manager; only the Secretary renders it.
- secretary.ts `needsOverdue` and the decision run both return null unless `rankSchedule(world)` is active with retainer "funded". With sc_8zoclbtrwp ended, no backstop run and no decision run is ever made.
- secretary.ts `ensureRankSchedule`: "made once: never made again once any exists (ended or rejected included)". So the lapse is permanent until code changes.
- schedules.ts: "a schedule is renewed on purpose", but nothing tells anyone a retainer is about to end, and an ended schedule cannot be renewed.
- Captain requests have no fallback view: the HUD lists pending access requests for admins (hud.tsx usePendingAccess), but captain requests show only in the goal tree panel (GoalTreePanel.tsx).

## What it means for the goal
"Starting from their first visit": a stranger's two doors (ask to join, ask to captain) end in a request that no human sees in the decision queue. Since 11-18, every manager need left unrendered also has no backstop.

## Inferred, not verified
- Whether Mitchell meant the ranking schedule to end. Nothing in the 1:1 notes I found says so; rankOnFiling (#527) ranks new asks in code, which may make the daily ranking less needed, but not the backstop.

## Not known
- How many access requests are pending: /api/access-requests returned an object I did not parse fully.
