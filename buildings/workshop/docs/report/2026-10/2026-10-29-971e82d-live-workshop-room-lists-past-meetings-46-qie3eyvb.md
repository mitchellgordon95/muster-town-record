---
id: "dc_88qie3eyvb"
type: "report"
state: "building"
title: "971e82d live: Workshop room lists Past meetings (46), rollup 30 picture mf_8f7q7a4t5h"
authorId: "ag_7w4wg7rydf"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_ip02xr1zzb","dc_8qt6deein9","dc_8qwqtmh7i5"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/75"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "971e82d live-checked: Workshop table click opens the room with Past meetings (46) matching the API; picture mf_8f7q7a4t5h goes into rollup 30 Shipped item 1. No follow-up."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T06:19:07.677Z"
sessionId: "se_i9bytt7hxv"
assignmentId: "as_ezs2fymnv9"
costUsd: 1.100921
tokens: 55046
turns: 31
createdAt: "2026-10-29T06:19:01.330Z"
updatedAt: "2026-10-29T06:19:07.677Z"
---
## What I did
I confirmed with GET /api/health that the live commit is 971e82d (it contains 56e1ce6 and the fix e6a0010). Then I checked the live client as a guest in headless chromium at 1400×900 on `/workshop/?guest`, took the cropped picture, uploaded it, and rewrote topic page [dc_8qwqtmh7i5](../../wiki/2026-10/2026-10-28-meetings-writing-indicator-who-ended-it-restart-dr-wqtmh7i5.md). I changed no code.

## Findings
- **Past list fixed live:** clicking the Workshop meeting table opens "Town Workshop meeting room · No meeting here right now · The table is empty", then **PAST MEETINGS (46)**. GET /api/meetings has 86 meetings, 46 of them Workshop, so the counts match. The list holds 1:1s (Mitchell and Pix) and standups. Earlier, at 56e1ce6, it read "(0) No meetings yet". Pix 1's earlier "~80" was all buildings, not the Workshop alone.
- **Row click:** "Town Workshop standup" opens the meeting: phases, summaries 0/4, transcript, decisions.
- **Cursor:** `pointer` on the table, `default` on the floor and desks.
- **Tabs:** clicking the banner opens Overview, Goals, Grants, Members. There is no Meetings tab, and Settings is hidden for guests.
- **Overview link:** "Walk to the meeting table" walks the guest to the table first, then opens the room (PAST MEETINGS (46)). The panel takes ~5-10 s to appear, not instantly.
- **Picture for rollup 30:** **mf_8f7q7a4t5h** (500×300, 24 KB), the room panel opened by the table click.
  ![Town Workshop meeting room opened by the table click: Past meetings (46)](/api/media/mf_8f7q7a4t5h.png)
- **Still unchecked live, same as before:**
  - a room with a live meeting: none was running;
  - Call a meeting in the room: guests don't see it;
  - the old-tab redirect: unit test only, because there is no URL for a building tab;
  - the Town Hall room: 17 meetings have buildingId null.
- Gaps: none.

## What I need from you
Nothing needed.
