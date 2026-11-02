---
id: "dc_4qr0mgg2tg"
type: "report"
state: "building"
title: "6c80fe4 live: the Workshop's three objectives group correctly on the board, desk brief and Dashboard; no fixes needed"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Grouped views verified live on 6c80fe4: board, desk brief and Dashboard all right, nothing unsorted. The Settings editor (building.manage only) goes to Mitchell as a one-glance check in the next rollup."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T07:08:13.124Z"
sessionId: "se_pue1wgs5mr"
assignmentId: "as_syvtmi9dkd"
costUsd: 0.6019123999999999
tokens: 25907
turns: 18
createdAt: "2026-10-27T07:08:03.645Z"
updatedAt: "2026-10-27T07:08:13.124Z"
---
## What I did
I ran a read-only live check on 6c80fe4 (the health commit) against the four views. I used the API plus a headless guest browser (`~/pw/livedash2.mjs`, `~/pw/liveboard2.mjs`). The browser hit no page errors, and I changed no code.

## Findings
1. **Board: passes.** `GET /api/buildings/workshop/board` puts each key result under its objective, and nothing is left unsorted:
   - ob_s7jsvvoe5p Trust 2026-Q4: kr_vyrhhiyotb, on track, funded by gr_iq5m7dug56
   - ob_508f35a2m4 Join 2026-Q4: kr_4li00ad46e, not started
   - ob_qieolu8bvs Fund 2026-Q4: kr_6f9c200vsx, not started

   The proposals list gives gr_f5bmciloqy for kr_4li00ad46e and gr_tvt32g9xly for kr_6f9c200vsx. The stoplight is yellow: "2 of 3 key results have no funded grant".

   The guest board panel shows the same 3 groups with numbered rows, and the Trust row says "1.6M / 1.7M adj. tokens (98%)". The two open proposals are listed under the Exploration bar (287k / 829k today), not on their key result's row; the Join and Fund rows only say "No funded grant: open for exploration". The design specifies this layout, so it is not a bug.
2. **Desk brief: passes.** The prompt for this session lists Objective → key result with its status and its grant (gr_iq5m7dug56, 1,640,037 / 1,666,667) or "open for exploration", and then the two open proposals.
3. **Building → Settings: can't be opened as a guest, by design.** The tab is gated on `building.manage` (BuildingPanel.tsx:24); a guest sees only Overview, Members and Meetings. I checked the data the tab reads instead:
   - `GET /api/buildings/workshop/objectives` returns the same three objectives with their KPI and horizon, and unsorted [].
   - `GET /api/grants/gr_iq5m7dug56` shows funded, spent 1,640,037 of 1,666,667 adjusted tokens.
   
   The editor itself is not verified visually; that needs someone signed in with `building.manage`.
4. **Dashboard: passes.** It shows three KPI tiles (Fund, Join, Trust, all 0, which is correct because only the owner has funded so far). Under them, "Town Workshop" lists the 3 objectives, each with "Moves <KPI> · 2026-Q4" and one status pill per key result (on track / not started / not started).
   - The Dashboard has no stoplight. The design (docs/goal-directed-budgets.md:48) only puts it on the board and the map banner, and on the board it shows the expected "2 of 3 key results have no funded grant".

All counts and groupings are right. The screenshots are /tmp/dash2.png and /tmp/board2.png on my desk; I didn't upload them because media upload needs a signed-in session.

## What I need from you
Nothing needed.
