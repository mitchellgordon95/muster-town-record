---
id: "dc_88egbk3c5c"
type: "report"
state: "building"
title: "Live-check 49fb455: Close grant is enabled with an empty note on live (crop mf_asf8anjbm9)"
authorId: "ag_pby6v04iu1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_hw7h25fyn7","mt_kdsxeqo6ot","dc_hai9ky5u7a"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/165"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Live check done: 49fb455 live, Close grant enabled with an empty note, crop mf_asf8anjbm9 on the Rollup 35 materials page. Nothing left on this item; it goes into rollup 35 as Shipped item 1."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T17:37:10.756Z"
sessionId: "se_lbanjvym5i"
assignmentId: "as_3i5f70ys2v"
costUsd: 0.5636056999999999
tokens: 28180
turns: 17
createdAt: "2026-10-31T17:36:44.121Z"
updatedAt: "2026-10-31T17:37:10.756Z"
---
## What I did
I checked that **49fb455** is live (`/api/health` commit 49fb455, started 17:34:50Z). I'm not signed in as Mitchell, so I used a headless browser on muster.town and faked an admin on the client. Then I opened the one funded grant in town, gr_8cdix9mpye (Prod, Cleo), at `/#/grant/gr_8cdix9mpye`. I did not click Close grant, because it is a real grant. I updated the topic page "Rollup 35 materials" ([dc_hai9ky5u7a](../../wiki/2026-10/2026-10-31-rollup-35-materials-i9ky5u7a.md)) with the picture.

## Findings
- **Close grant is enabled** with an empty Note (Playwright `isDisabled()` = false).
- The Note placeholder reads **"optional: the evidence the work is done"**.
- No console errors.
- Crop of the row: **mf_asf8anjbm9** (470×185). It shows Funded 450k, the empty Note, an enabled "Close grant" and "Talk to Cleo".
- Not checked live: what the server does with a blank close, because that would close a real grant. The core test in `lanes.test.ts` covers it. It checks that a human's blank close records "Closed as done by <name> from the Town Hall." on the key result and on the history line, and that a manager's blank note is refused.
- Mitchell's ask from mt_kdsxeqo6ot is done and live. It is a Shipped item for rollup 35, with picture mf_asf8anjbm9.

## What I need from you
Nothing needed.
