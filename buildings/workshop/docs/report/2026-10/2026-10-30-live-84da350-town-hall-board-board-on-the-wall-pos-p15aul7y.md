---
id: "dc_ndp15aul7y"
type: "report"
state: "building"
title: "Live: 84da350 Town Hall board (board on the wall, Post a town-wide note, Take off the board)"
authorId: "ag_y8nzridye8"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_1tiugozhan","dc_ym8fjxqjiv","dc_jcyf86dpdp","dc_sfumqigkfa"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/107"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Live-checked 84da350 (Town Hall board, PR #107): health commit, board:town-hall place opens from the map, Post a town-wide note + Take off the board on all 5 FYIs, picture mf_46l1um7hyd. Flag dc_ym8fjxqjiv part 1 done; goes in rollup 31 Shipped with Pix 2's schedule-object work. Outbox dc_sfumqigkfa stays open for Mitchell to press Take off the board on dc_z22wolxdnu."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T01:16:49.831Z"
sessionId: "se_vxcr20xfja"
assignmentId: "as_pg4ob3zyf0"
costUsd: 0.8687277
tokens: 43436
turns: 22
createdAt: "2026-10-30T01:16:32.639Z"
updatedAt: "2026-10-30T01:16:49.831Z"
---
## What I did
Live-checked 84da350 (PR #107, part 1 of Mitchell's flag [dc_ym8fjxqjiv](../../flag/2026-10/2026-10-30-i-don-t-see-a-board-in-the-townhall-for-me-to-post-8fjxqjiv.md)) in a headless browser on https://muster.town. I took one cropped picture and uploaded it. I also rewrote topic page [dc_jcyf86dpdp](../../wiki/2026-10/2026-10-28-web-client-panels-and-the-in-tray-yf86dpdp.md), and the check script is on my desk at ~/demo/b84.mjs.

![Town Hall board live at 84da350](/api/media/mf_46l1um7hyd.png)

## Findings
- **Live commit:** /api/health shows commit 84da350 (server started 01:14:21Z). My own `look` lists the new place `board:town-hall` ("Town Hall board (town-wide FYIs)").
- **The board opens from the map:** a guest avatar walked to `board:town-hall`, I pressed `e`, and the Town Hall board panel opened. The board shows on the Town Hall's back wall, under the banner (see picture).
- **What the panel shows, as a fake admin:** I made the browser think it was signed in as an admin, using `window.musterTown.store.set({me:{… isAdmin:true}})`. The panel then showed:
  - the "Post a town-wide note" form (title, body, "Post to every building");
  - all 5 town-wide FYIs, each with author and age, e.g. "Pix · 20m ago": dc_fbwpcgi3zj, dc_6bxjb0oxzf, dc_z22wolxdnu, the rollup-format FYI dc_ygwvun6sd4 and the merge rules dc_xsrxxbfa7i;
  - "Take off the board" on all 5 rows.
- **Not checked:** a real sign-in posting a note or taking one off the board. Desks have no GitHub sign-in, so this check only covers what the browser shows; the server's write and unpublish routes were covered by tests in [dc_1tiugozhan](2026-10-30-town-hall-board-merged-pr-107-84da350-board-on-the-iugozhan.md).
- **Outbox [dc_sfumqigkfa](../../../../../town-hall/outbox/2026-10/2026-10-29-unpublish-the-stale-town-wide-fyi-dc-z22wolxdnu-re-umqigkfa.md)** can close as soon as Mitchell (or Pix, the author) presses "Take off the board" on dc_z22wolxdnu. The button is live now.
- The assignment is done.

## What I need from you
Nothing needed.
