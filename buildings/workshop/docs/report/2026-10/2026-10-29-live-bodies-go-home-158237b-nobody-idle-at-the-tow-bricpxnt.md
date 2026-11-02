---
id: "dc_n4bricpxnt"
type: "report"
state: "building"
title: "Live: bodies go home (158237b); nobody idle at the Town Hall meeting room, picture mf_y0g3hvpffn"
authorId: "ag_ihbmjd2n4d"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_ihwq7bfi4o","dc_xmclldi5j8","dc_8qwqtmh7i5"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/90"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "158237b live-checked: 9 residents on their desk tiles, walk-home events 10-14 s after restart, nobody but Mitchell and deskless visitors near the Town Hall meeting room. Picture mf_y0g3hvpffn is from the LIVE server. Flag dc_ihwq7bfi4o done end to end; rollup 31 Shipped candidate #3 is complete."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T21:34:14.993Z"
sessionId: "se_9uhz9z8ejw"
assignmentId: "as_lnwhlvbw89"
costUsd: 0.8260732000000001
tokens: 41304
turns: 25
createdAt: "2026-10-29T21:34:08.965Z"
updatedAt: "2026-10-29T21:34:14.993Z"
---
## What I did
I checked the live server, positions from GET /api/town and the event log after 158237b (PR #90, Mitchell's flag [dc_ihwq7bfi4o](../../flag/2026-10/2026-10-29-for-some-reason-i-see-a-bunch-of-managers-lingerin-wq7bfi4o.md)) went live. I took one cropped screenshot of the Town Hall map as a guest (headless) and rewrote the topic page [dc_8qwqtmh7i5](../../wiki/2026-10/2026-10-28-meetings-writing-indicator-who-ended-it-restart-dr-wqtmh7i5.md).

## Findings
- **Live commit:** GET /api/health shows commit 158237b640bb…, started 21:31:04Z.
- **Walk-home events:** the event log has `agent.moved` events from the new idle tick, all 10–14 s after the restart:
  - Pix walked to Pix's desk (21:31:14Z).
  - Kelly walked to Kelly's desk (21:31:15Z).
  - Nell walked to Nell's desk (21:31:16Z).
  - Mara walked to Mara's desk (21:31:18Z).
  - Pix had last walked to Mitchell's flag at 21:19Z.
- **Positions (GET /api/town, 21:31Z):** all 9 residents stand exactly on their own desk tile: Pix, Kelly, Cleo, Nell, Mara, Pix 1, Pix 2, Pix 3 and Cleo 1.
- **Meeting room:** within 3 tiles of the Town Hall meeting room (59,34) there are only:
  - Mitchell (human).
  - Three offline visitors: Claude Code, CI and mitchellgordon95's Claude. They have no desk, so they keep the old behaviour, as the flag specified.
- **Picture for rollup 31:** ![Town Hall meeting table after 158237b: no residents](/api/media/mf_y0g3hvpffn.png) (mf_y0g3hvpffn, 390×300). It shows the meeting table with Mitchell and the sleeping visitor bodies and no residents.
- **Not checked live:** a meeting ending and its attendees walking home, because no meeting ran in this window. The code path is covered by core test/walk-home.test.ts.
- Flag [dc_ihwq7bfi4o](../../flag/2026-10/2026-10-29-for-some-reason-i-see-a-bunch-of-managers-lingerin-wq7bfi4o.md) is done end to end. Chain as_rx4w0sc7sw is complete.

## What I need from you
Nothing needed.
