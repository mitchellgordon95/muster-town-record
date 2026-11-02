---
id: "dc_drey0vkcb4"
type: "report"
state: "building"
title: "Town Hall \"User stats\" stand pushed to main (6eb6560); live check parked on its deploy"
authorId: "ag_ii05y41psy"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: 6eb6560 on main (Mitchell's mt_ec2b7x80rg decision 2), tests green, Pix told. Live check already parked as as_wyr76zz4xw on deploy 6eb6560 (two pictures + manual re-seed check on resume). Rolls up with the Dashboard removal and the goal-tree docs once live and checked."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-01T02:20:07.936Z"
sessionId: "se_w8jt30mrxs"
assignmentId: "as_uvkh7ghqru"
costUsd: 2.7917988999999994
tokens: 139590
turns: 61
createdAt: "2026-11-01T02:19:57.333Z"
updatedAt: "2026-11-01T02:20:07.936Z"
---
## What I did
Built Mitchell's decision 2 from 1:1 mt_ec2b7x80rg ("user stats lives somewhere in the town hall on its own object… make the outbox table smaller") and pushed it straight to main as **6eb6560**. Ran typecheck, knip, the web tests (217) and the core furniture, layout and map-shapes tests; all passed. Checked it in mock mode at 1400×900 and 390×844 with 0 console errors. Told Pix about the layout change (ms_okf24v47za). Topic page: [dc_ze5o8drnl9](../../wiki/2026-11/2026-11-01-user-stats-stand-town-hall-5o8drnl9.md).

## Findings
- **Layout:** the outbox counter is now 2 tiles instead of 4, and its standing spot (3,7) is unchanged. A new place `stats` (TILE.STATS 33, an easel with funnel bars) sits at Town Hall lot (5,6) and is used from (5,7). The in-tray, the Bank and every other piece are where they were. Tests check that every place is reachable in every map shape. Hosted collectives use the same layout code, and the live Workshop and Hollyville Town Halls have no moved furniture, so both get the stand.
- **Panel (E "Read the user stats", panels/StatsPanel.tsx), in this order:**
  - 30-day totals: saw card, signed in, asked, let in, declined, typical wait.
  - By day: a compact table summed over collectives, newest first.
  - Per collective: only on the root server. A hosted collective's /api/join-funnel lists only itself, so the table is hidden there.
  - What each number is, including that guest-card views are rough.
  - A JSON link to the endpoint.
- **Other changes:**
  - Short waits now read in seconds ("15 s"). This fixes the old nit where 15 s showed as "1 min".
  - Adding an "acted" column later is one entry in `COLUMNS`.
  - `JoinFunnelView` now types `collectives[]` with their daily rows.
  - The mock serves Workshop and Hollyville numbers.
- **Docs:**
  - manual.md has one line for the stand. A rebase onto upstream pushed the manual 1 word over its cap, so I trimmed other lines; it is now 1,887 of 1,900 words.
  - goal-directed-budgets.md now points to the stand instead of the Dashboard.
  - The live manual doc ([dc_irk1w62mpv](../../../../../library/article/2026-10/2026-10-27-operating-manual-k1w62mpv.md)) re-seeds from the repo on boot when nobody has edited it in town; I'll check that on resume.
- **Mock pictures (desk only):** the stand beside the shortened counter, and the panel. On phone the per-collective table scrolls sideways.
- **On resume (recipe [dc_bci4l87ab6](../../wiki/2026-10/2026-10-29-live-verification-on-muster-town-i4l87ab6.md)):**
  - Confirm 6eb6560 is live.
  - At 1400×900 and 390×844: `musterTown.walkTo("stats")`, press E, 0 console errors.
  - Take two cropped pictures of 300 px or less: one of the stand in the Town Hall, one of the panel.
  - Repeat at /hollyville/.

## What I need from you
Nothing needed.
