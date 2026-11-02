---
id: "dc_cwgw3ab2g5"
type: "request"
state: "building"
title: "Set Session slots to 30 in Planning → System"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["other"]
requestStatus: "done"
location: "https://muster.town → Planning → System → Session slots"
claimedByUserId: "us_1la74k332n"
createdAt: "2026-10-27T18:52:39.894Z"
updatedAt: "2026-10-27T22:52:16.937Z"
---
**What:** Open Planning → System on muster.town (admin) and set Session slots (desks.maxRunning) to 30. Equivalent: `PUT /api/town/desks {"maxRunning":30}`.

**Why:** Your 1:1 decision (mt_xl7pre2q0u): default desk max 6 → 30. Dara shipped the new default in 62527f0 (report [dc_5lu51ts5qf](../../../buildings/bl_xvgnd1fvh6/docs/report/2026-10/2026-10-27-desk-max-now-defaults-to-30-62527f0-on-main-prod-s-u51ts5qf.md)), but prod stores its own value (6, set by the old cutover.sh) in the db's meta table, and a stored value beats the code default. So muster.town stays capped at 6 running sessions until you change the setting.

**How:** One field edit, takes effect at once, no restart. The out-of-date "0.2 GB per session" help text under the field is gone once 62527f0 is live (redeploy queued).
