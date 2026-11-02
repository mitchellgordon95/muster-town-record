---
id: "dc_ze5o8drnl9"
type: "wiki"
state: "building"
title: "User stats stand (Town Hall)"
authorId: "ag_ii05y41psy"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_hzjw0z0zlz"
createdAt: "2026-11-01T02:19:44.217Z"
updatedAt: "2026-11-01T02:30:10.441Z"
---
State 2026-11-01: **6eb6560 LIVE and checked** (in live 244d9d1, server started 2026-11-01T02:26:15Z; check as_wyr76zz4xw). Pictures: stand mf_r1deqt80ux, panel mf_r40zfuzumf. Source: Mitchell 1:1 mt_ec2b7x80rg decision 2 (replaces the Dashboard's funnel row, removed in 7ad702d). Build report [dc_drey0vkcb4](../../report/2026-11/2026-11-01-town-hall-user-stats-stand-pushed-to-main-6eb6560-ey0vkcb4.md).
## What exists
- Place `stats` (kind "stats", TILE.STATS 33): an easel with funnel bars at Town Hall lot (5,6), stand (5,7). Outbox counter is 2 tiles (2,6)-(3,6), stand (3,7). core furniture.ts / layout.ts; mock web/src/mock/layout.ts. Same in every map shape and hosted collectives.
- E "Read the user stats" → panels/StatsPanel.tsx: 30-day totals (saw card, signed in, asked, let in, declined, typical wait), By day (newest first), Per collective (root server only), definitions, JSON link to `${API_BASE}/api/join-funnel`. Waits under a minute read in seconds.
- An "acted" column (gr_58n37j410s step 3) is one entry in StatsPanel `COLUMNS` plus the server field.
- Tests: core furniture.test.ts, map-shapes.test.ts, web statsPanel.test.tsx. Manual line under Town Hall objects.
## Live check result (2026-11-01)
Workshop and /hollyville/ at 1400×900 and 390×844: walkTo("stats") true, E opens the panel, 0 console errors. Workshop shows Per collective (workshop, hollyville); Hollyville shows only its own numbers with no Per collective table. Once at desktop, the first E press right after the walk did not open the panel (the prompt was showing "Tab next 2/2"); on a rerun it opened. Probably a timing race in the headless run; not reproduced.
## Re-check recipe
[dc_bci4l87ab6](../2026-10/2026-10-29-live-verification-on-muster-town-i4l87ab6.md) (puppeteer-core lives at /home/agent/kr2tool on Kelly 1's desk).
