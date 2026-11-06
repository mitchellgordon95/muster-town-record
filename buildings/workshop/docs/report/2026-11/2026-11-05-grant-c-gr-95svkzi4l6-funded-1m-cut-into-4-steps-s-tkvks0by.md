---
id: "dc_tctkvks0by"
type: "report"
state: "building"
title: "Grant C gr_95svkzi4l6 (funded 1M) cut into 4 steps; step 1 (delete the checkpoint session and checkpoint_grant, reserve hold point, tests) queued to the building as as_xg977jopw3 behind grant B step 1"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_nqgbjho18g","dc_ri656aimsj","dc_g1ov1tdtvv"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Grant C kickoff done: step 1 as_xg977jopw3 queued behind grant B step 1 (as_vw7fmyi8ew, same files). Nothing further to assign; folds into the next rollup once B/C step 1 land."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T22:03:31.654Z"
sessionId: "se_seunbj5asd"
assignmentId: "as_8kujm9vxnj"
costUsd: 1.3668665
tokens: 68343
turns: 11
createdAt: "2026-11-05T22:03:12.800Z"
updatedAt: "2026-11-05T22:03:31.654Z"
---
## What I did
Read the plan ([dc_nqgbjho18g](../../wiki/2026-11/2026-11-05-grant-c-self-assembling-checkpoint-card-reserve-gbjho18g.md)) and my grant C page (dc_ri656aimsj), checked what Pix 1 is doing on grant B step 1 (as_vw7fmyi8ew: rewriting core grants.ts and verbs/docs.ts, no PR yet), and cut grant C into 4 steps. Step 1 went on the building queue as **as_xg977jopw3** (lane grant, gr_95svkzi4l6, pages [dc_nqgbjho18g](../../wiki/2026-11/2026-11-05-grant-c-self-assembling-checkpoint-card-reserve-gbjho18g.md), [dc_lq9eo4lz5a](../../wiki/2026-11/2026-11-05-grant-b-steps-in-the-proposal-no-kickoff-session-9eo4lz5a.md), [dc_oghes5lgud](../../wiki/2026-10/2026-10-28-grants-key-results-and-the-town-hall-in-tray-hes5lgud.md)) with **waitFor {assignment: as_vw7fmyi8ew}**, so it starts only after grant B step 1 finishes: both edit the same two core files and a race would cost a rebase or undo B's work. Rewrote the grant C wiki page with the four steps; logged it.

## Findings
The steps, one owner each, each with a live check:
1. **Core + tests (as_xg977jopw3, queued):** delete checkpointAssignment, cancelCheckpointAssignment, fileCheckpoint, the checkpoint_grant verb, schema, route, describe and prompt mentions, and the lanes.ts exception that let the checkpoint session run during a hold. Reserve = min(150k, a third): a funded grant holds at grant − reserve, continue holds again at 100%, adjust recomputes, a grant already held stays as it is, no sweep. GET /api/grants/<id> returns holdAtTokens and the grant card shows "holds at N". Bank claim, earmarks and overdraft walk untouched (Mitchell's funding at 1M is his yes to the hold-point change). Serves kr_dltzqgqo78, kr_tfm8zlvr08, half of kr_jnkstduw76.
2. **submit_report evidence + card/deck** (queued after step 1's report): keyResults and topUp fields on submit_report, grant lane and own grant only; evidence() and the deck slide list the grant's reports and each key result's fork note, "No evidence filed by the forks" when none; fork prompt tells forks to file it. Serves kr_13txlz2pnc, kr_z0gd978wbg, the rest of kr_jnkstduw76.
3. **Live check** on the first holds after it lands (parked up to 5 days; stops early if fewer than 2 holds, per the stop condition).
4. **Close** with the evidence and a rollup.

Grant B step 1 was at 40k tokens and 2 minutes in when I looked; C step 1 should start within the hour.

## What I need from you
Nothing needed.
