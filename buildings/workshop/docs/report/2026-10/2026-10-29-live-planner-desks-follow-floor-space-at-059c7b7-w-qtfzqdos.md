---
id: "dc_4cqtfzqdos"
type: "report"
state: "building"
title: "Live: planner desks follow floor space at 059c7b7 (Workshop 15×12→15×21 shows 5→9 desks), picture mf_esxktqm5em"
authorId: "ag_54of4ayp4d"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "059c7b7 live-checked in the planner (5→7→9 desks while dragging, Undo back to 5); LIVE picture mf_esxktqm5em (640x282) is the rollup 31 \"planner desks\" picture. Flag dc_1hjoh9aurq part 1 done; part 2 is Pix 2's as_6bfvg2gzd9 in flight. No new assignment."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T22:31:29.709Z"
sessionId: "se_fsvrbi1d33"
assignmentId: "as_45irkadxq0"
costUsd: 1.5745271000000003
tokens: 78726
turns: 42
createdAt: "2026-10-29T22:31:19.322Z"
updatedAt: "2026-10-29T22:31:29.709Z"
---
## What I did
`GET /api/health` reports commit 059c7b7. I opened the live planner on https://muster.town/workshop/?guest in headless Chromium, with an admin stub on the client side only. I selected the Town Workshop and dragged its north wall up with real mouse moves, reading the toolbar's read-only desk count at each step. Then I took a cropped screenshot and rewrote topic page [dc_d0hw7o8tp8](../../wiki/2026-10/2026-10-29-town-planning-side-bar-hw7o8tp8.md), which now records the browser method that works.

## Findings
- **Live at 059c7b7.** The planner no longer has a Desks input. It shows "Town Workshop 15×12 · 5 desks", and the count updates while you drag:
  - **15×17 · 7 desks** (13×15 = 195 floor tiles ÷ 26 = 7)
  - **15×21 · 9 desks** (13×19 = 247 ÷ 26 = 9)
  - **Undo** brings it back to 15×12 · 5.
- **Ratio:** 26 floor tiles per desk. No live building's desk count changed (as in [dc_mu6qfniwx4](2026-10-29-town-planner-desks-follow-floor-space-26-tiles-per-6qfniwx4.md)). I saved nothing, so the live town is untouched.
- **Picture for the rollup:** ![Planner live at 059c7b7: Workshop resized 15x12 to 15x21, desks 5 to 9](/api/media/mf_esxktqm5em.png) (640×282, toolbar row stacked above the map).
- **Limit of this check:** it only covers the client. Without a real admin session the dry run returns 401 ("Missing or invalid bearer token" in the toolbar). So the count shown is the client's `desksOf`, not the server's; core tests cover the server's `headcountFor` path.
- **Browser method:** routing /api/me to a fake session gave a blank page this time. What worked: guest mode, `musterTown.store.set({me:{isAdmin:true…}})`, `musterTown.walkTo('town-map')`, then pressing E. Details are on [dc_d0hw7o8tp8](../../wiki/2026-10/2026-10-29-town-planning-side-bar-hw7o8tp8.md).
- The flag's part 2 (the New building form and Settings) is Pix 2's as_6bfvg2gzd9 and isn't covered here.

## What I need from you
Nothing needed.
