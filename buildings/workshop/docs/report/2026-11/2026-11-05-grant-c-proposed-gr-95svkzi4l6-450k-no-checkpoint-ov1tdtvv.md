---
id: "dc_g1ov1tdtvv"
type: "report"
state: "building"
title: "Grant C proposed: gr_95svkzi4l6 (450k): no checkpoint session, card assembles from fork evidence, reserve moves the hold point"
authorId: "ag_wgv47frvu7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_y949h9jto6","mt_o0exccdv8g","dc_nqgbjho18g","dc_p73nckwcta"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Grant C proposed as gr_95svkzi4l6 (450k, 5 KRs due 11-09/11-10; plan dc_nqgbjho18g); it reaches Mitchell in the Town Hall in-tray on its own, with the hold-point change flagged for his yes in the note. The measurement (18 holds, median 108k per checkpoint session, ~3.33M booked past 100% over 17 grants) is the case. Evidence via submit_report fields over a new tool is the right smallest mechanism. Nothing further."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T21:53:52.640Z"
sessionId: "se_eiq65fiv3m"
assignmentId: "as_yswef29vav"
costUsd: 1.6063998
tokens: 80320
turns: 33
createdAt: "2026-11-05T21:53:46.162Z"
updatedAt: "2026-11-05T21:53:52.640Z"
---
## What I did
I read the checkpoint path: core grants.ts (checkpoints, checkpointAssignment, fileCheckpoint, evidence), the hold in lanes.ts, the checkpoint-rollup link in verbs/docs.ts, the card (web Places.tsx and core review-deck.ts) and the Bank claims in free-tokens.ts. I measured every 100% hold since 10-31 from the live API. I wrote the plan as topic page [dc_nqgbjho18g](../../wiki/2026-11/2026-11-05-grant-c-self-assembling-checkpoint-card-reserve-gbjho18g.md) and filed **gr_95svkzi4l6** (450k, goal gl_join). Nothing is built.

## Findings
**The cost today.** There have been 18 holds at 100% since 2026-10-31.
- "Write the checkpoint" sessions: median **108k** adjusted tokens each (range 49–204k), about **2.1M** in total.
- Sessions still running when the hold fired added about **1.4M**.
- Together that is a median **145k booked past 100% per grant**, about **3.33M over 17 grants**. Every hold ends past 100%, because the hold only fires after the session that crosses it.

**The plan** (on [dc_nqgbjho18g](../../wiki/2026-11/2026-11-05-grant-c-self-assembling-checkpoint-card-reserve-gbjho18g.md)):
1. **Delete the checkpoint session, with no fallback.** That removes the checkpoint assignment, the lane exception that lets it run during a hold, the checkpoint_grant tool and fileCheckpoint, and the checkpoint-rollup link.
2. **Forks file evidence in `submit_report`.** It gets two optional fields:
   - `keyResults [{id, status up to claimed, evidence}]`
   - `topUp {tokens, buys}`

   They are accepted only from a grant-lane session, for its own grant's key results. They write the key result's existing status note, with the report id and the fork as author.
   - I chose this over a new tool because the fork already makes that call when it knows what shipped: no extra turns, the evidence stays tied to its report, and no new table.
3. **The card and the deck slide assemble from that data:** a line per key result, the grant's reports, spend and the top-up line. With no evidence the card says "No evidence filed by the forks" and the top-up line is empty.
4. **Reserve = min(150k, a third of the grant).** The hold fires at the grant's tokens minus the reserve. Continue holds again at 100%, and adjust recomputes the reserve.
   - The Bank claim stays grantTokens − spent, so free tokens, earmarks and the overdraft walk do not change. Only when the hold fires changes.
   - The forks still running at past holds booked 44k, 45k, 95k, 137k, 138k, 152k and 269k. This reserve would have covered 5 of those 7.
5. **Cutover:** a grant already held stays as it is. Every funded grant gets the reserve from the day C lands.

**The five key results:** kr_dltzqgqo78 (no checkpoint session), kr_13txlz2pnc (fork evidence), kr_z0gd978wbg (card and deck), kr_tfm8zlvr08 (at least 4 of the first 5 holds at or under the grant's tokens), kr_jnkstduw76 (tests). They are due 11-09 and 11-10.

**Estimate line:** 3 similar grants spent 189k–950k; median spent/funded is 0.90.

The proposal note asks for Mitchell's yes on the hold-point change under the merge rules.

## What I need from you
Nothing needed.
