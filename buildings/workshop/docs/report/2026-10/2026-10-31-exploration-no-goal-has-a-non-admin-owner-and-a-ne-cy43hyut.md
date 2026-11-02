---
id: "dc_arcy43hyut"
type: "report"
state: "building"
title: "Exploration: no goal has a non-admin owner and a newcomer can't ask for one; proposed gr_bwm0iz7rwl (\"Ask to own this goal\")"
authorId: "ag_bxupwa9njd"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_sudfbb4hvq","dc_ivddd9lih7","dc_nhd0maw3f5","dc_6mclou9rvg"],"urls":["https://muster.town/api/goals"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. gr_bwm0iz7rwl goes to Mitchell through the Town Hall in-tray on its own; kr_j1w17nw178 is listed in rollup 35 for him to keep or cut. Nothing queued until he decides."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T19:55:12.739Z"
sessionId: "se_cuz1s0fowq"
assignmentId: "as_lbba4j04az"
costUsd: 0.995374
tokens: 49769
turns: 24
createdAt: "2026-10-31T19:55:01.317Z"
updatedAt: "2026-10-31T19:55:12.739Z"
---
## What I did
I went through the open key results under gl_join. Three of them I ruled out:
- Town blockers (kr_hj8wwx0q0w): edition 7 already exists, so it only needs claiming.
- Deck (kr_2qg0ayfs1j): live.
- Starter brief (kr_4li00ad46e): blocked on Mitchell's visitor-shape choice ([dc_ivddd9lih7](../../wiki/2026-10/2026-10-28-visitor-agent-reports-ddd9lih7.md)).

Instead I checked the goal's core promise, "a human can own a piece of the goal tree ... from their first visit", against main (49afcdd) and GET /api/goals on muster.town. Findings are in [dc_sudfbb4hvq](../../note/2026-10/2026-10-31-findings-nobody-but-the-admins-owns-a-goal-and-a-n-dfbb4hvq.md). I wrote key result kr_j1w17nw178 and proposed grant gr_bwm0iz7rwl.

## Findings
- The owner features are built: ownerId, ownership passed down to child nodes, owner-scoped goals.edit and funding, in-tray routing, and Mine/All in the in-tray and the deck. But all 19 live goal nodes have ownerId null, so none of it has run with a second human.
- Only an admin can set an owner. Nothing lets a member ask for a node. Ask to join (core access.ts, PR #97) is the pattern to reuse.
- gr_bwm0iz7rwl, 600k tokens, covers three things: an "Ask to own" request routed to the node's current owner and decided in the in-tray or deck, which sets ownerId; tests and docs; and one live run with a second GitHub account through join → ask → accept → Mine → Fund.
- If Mitchell prefers to assign owners himself, the grant should be rejected and kr_j1w17nw178 cut.

## What I need from you
Decide gr_bwm0iz7rwl: fund it, or reject it if only admins should assign goal owners.
