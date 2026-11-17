---
id: "dc_q48pbvg0td"
type: "report"
state: "building"
title: "Why Outreach ran no exploration: root explore off for 6 days, then the town cap filled before its turn"
authorId: "ag_k7jo39j1vp"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Checked explore.ts:150: the tick walks buildings.all() in table order, so under a tight cap the last rowids (UI/UX, Outreach) are starved every day. Fairness fix queued as its own assignment; Juno already told."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-17T04:17:23.370Z"
sessionId: "se_1q68z1qdth"
assignmentId: "as_ws6fu05s91"
costUsd: 1.2602202
tokens: 63011
turns: 34
createdAt: "2026-11-17T04:16:46.471Z"
updatedAt: "2026-11-17T04:17:23.370Z"
---
## What I did
I read the explore tick in packages/core/src/explore.ts and free-tokens.ts. Then I checked the live town for Outreach (bl_6ifesdbah3): its goal, queue, grants, events and sessions. I compared it with the five buildings that explored today. I told Juno the result (ms_jn6gs9810b).

## Findings
Outreach's own dials are fine. It is attached to gl_inx99nrlk5 under gl_town. No goal on that path sets explore, a chunk size or desksTotal, so it inherits explore on and a 100k chunk. It has 2 desks and nothing queued or held. It had no open proposal until 03:49Z. There are 16.08M free tokens. Three things blocked it, one after another:

1. **Exploration was off town-wide from 11-10 20:29:58Z to 11-17 03:26:10Z.** Mitchell switched explore off on gl_town (event 145499) and back on at 03:26:10Z (event 166767). In that window `exploreBlock` returns "exploration is off" for every building, so nobody explored for six days.
2. **When it came back on, the town-wide cap filled before Outreach's turn.** `exploreTick` (explore.ts:150) visits buildings in rowid order: Workshop, Onboarding, Prod, Bank, Code Legibility, UI/UX, then Outreach last. At 03:26:11Z the first four each reserved 100,000 (events 166769, 166771, 166773, 166775). `exploreSpentToday` (free-tokens.ts:218) counts open reservations at full size, plus every exploration-lane session today. That included Code Legibility's 92,145 tokens from 02:00-02:12Z (as_b0rowagpl7, as_ascuy3d4zt, as_lrkxspzs39). So spent was 400,000 + 92,145, and one more chunk would pass the 500,000/day cap on gl_town. Code Legibility, UI/UX and Outreach were refused. After the chunks closed, the next tick at 03:30:13Z gave the free slot to Code Legibility, which comes first in the order (as_dgv69032kr). After that the cap never had room for another 100k. Exploration used today is **553,659 of 500,000**, per /api/health budgets. 301,406 of it is Code Legibility, mostly live checks and fixes filed in the exploration lane (as_bx6farp8ou, as_5ishd5x5e5, as_wewikisb1d and the three above), not tick explorers. UI/UX also has 0 today for the same reason.
3. **Since 03:49:50Z Outreach's own proposal blocks it.** Juno filed gr_qholnel3q4 (450k) from Mitchell's 1:1, and the rule "a proposal of this building is open and undecided" applies until Mitchell funds, counters or rejects it.

**What turns it back on:**
- Nothing is broken. The cap resets at 00:00Z. Once gr_qholnel3q4 is decided, Outreach can explore when it has a free desk and nothing queued. If the grant is funded, its steps will fill the desks first.
- A dial Mitchell can flip: raise the 500k cap on gl_town, or give subtrees their own caps.
- A fairness fix I propose but did not code (no PR under this assignment): explore.ts:150 should visit buildings least-recently-explored first, ordered by their last bank_reservations openedAt, with never-explored first. Then a tight cap rotates across buildings instead of always starving the last rowids. Separately, managers who file routine live checks in the exploration lane use up the shared cap. Code Legibility did this for 209k today.

## What I need from you
Nothing needed. To give Outreach a turn before 00:00Z, Mitchell can raise the gl_town exploration cap and decide gr_qholnel3q4.
