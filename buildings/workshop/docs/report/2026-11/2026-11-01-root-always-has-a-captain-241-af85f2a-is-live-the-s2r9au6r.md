---
id: "dc_l5s2r9au6r"
type: "report"
state: "building"
title: "Root always has a captain (#241 = af85f2a) is live: the root's captain is Mitchell and the whole in-tray routes to him"
authorId: "ag_5otsojx96u"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "D7 live and checked (root captain Mitchell, in-tray routes to him); rollup 37 item 10."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-01T02:21:51.395Z"
sessionId: "se_lglmt4nlv3"
assignmentId: "as_18e5gsfqkx"
costUsd: 0.9061291
tokens: 45306
turns: 26
createdAt: "2026-11-01T02:20:52.649Z"
updatedAt: "2026-11-01T02:21:51.395Z"
---
## What I did
Checked that af85f2a is live: GET /api/health read 08c16a7 at 02:18:15Z, and 08c16a7 contains af85f2a. Then I checked the live API and the guest goal tree, and uploaded a picture. I added item 10 to the Rollup 37 materials ([dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md)) as a Shipped candidate. Item 8's "Your call" no longer applies, so I changed it to none. I also rewrote the topic page [dc_roeig7abhg](../../wiki/2026-11/2026-11-01-root-goal-always-has-a-captain-mt-cyd2t5ioob-d7-eig7abhg.md).

## Findings
- **The API shows Mitchell as the root's captain.** GET /api/goals returns root gl_town with ownerId us_1la74k332n, owner name "Mitchell". Before this change it was null.
- **In-tray routing:** GET /api/buildings/town-hall/intray sends all 10 current items to goal gl_town and captain Mitchell. Those are 3 proposals (gr_dt1l35tydx, gr_zsm1piyqyx, gr_60wpsdot41), 2 checkpoints (gr_ukrou4zjha, gr_mjr7nb438v) and 5 closed grants. "Mine" now means only "the item is routed to the viewer", so Mitchell's Mine holds those 10. I read the in-tray with an agent token, so I didn't see Mine as Mitchell does: for my token every item had mine=false, because I am not the captain. defaultView stays "all" for admins.
- **Guest goal tree:** the root box has the badge "👤 Mitchell" and the detail panel shows "Captain: Mitchell". Picture: mf_giidd18l6e (live, guest view, 44% zoom).
- **What is still admin-only is about permission, not routing:** funding (needs building.fund), editing goals (needs goals.edit), deciding captain requests (also goals.edit), and admins opening the in-tray on All. Captain requests at the root are now allowed, and they go to Mitchell.
- The D7 work is finished.

## What I need from you
Nothing needed.
