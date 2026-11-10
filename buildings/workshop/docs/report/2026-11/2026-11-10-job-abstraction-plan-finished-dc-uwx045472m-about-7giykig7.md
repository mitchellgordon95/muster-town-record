---
id: "dc_in7giykig7"
type: "report"
state: "building"
title: "Job abstraction plan finished (dc_uwx045472m): about 3.45M in total, stop point after step 5b at about 1.7M"
authorId: "ag_ur35rbd0a6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_uwx045472m","dc_ejm1j7m3r8","dc_kft2962dq9","mt_ewxnhs90cq","mt_db6itzy2br","dc_pqrcy8pmke"],"urls":[]}
tags: []
verdict: "pivot"
decision: "pending"
sessionId: "se_pmxzzcwvy0"
assignmentId: "as_kuxyjwh6a3"
costUsd: 1.8284046
tokens: 91420
turns: 29
createdAt: "2026-11-10T20:25:43.970Z"
updatedAt: "2026-11-10T20:25:43.970Z"
---
## What I did
I built the inventory table with grep and Read at main b12cc372, without subagents. I then corrected the cost estimates and wrote the full plan, with a one-minute summary at the top, as **[dc_uwx045472m](../../note/2026-11/2026-11-10-plan-the-job-abstraction-plan-and-cost-for-mitchel-x045472m.md)**.

The draft [dc_ejm1j7m3r8](../../note/2026-11/2026-11-10-plan-the-job-abstraction-draft-inventory-table-unf-m1j7m3r8.md) could not be updated in place, because the town refuses edits to another fork's document. The new doc supersedes it and cites it.

I also rewrote the topic page [dc_pqrcy8pmke](../../wiki/2026-11/2026-11-10-job-abstraction-plan-as-qganrass1j-rcy8pmke.md). No code was changed and there is no PR.

## Findings
- **One object, one loop.**
  - Every piece of work becomes a **job** with a single budget rule: chunk, ceiling, per-run, pocket or building.
  - The job's record is a thread of **entries**, and each entry has a new "what is left" field.
  - Each entry is settled at the lowest level that can: code first, then the manager, then the human at the nearest captained goal. Passing an entry up adds a note and creates nothing new.
- **What goes away:**
  - Rollups.
  - The six town-written ask templates in asks.ts (lines :272, :307, :323, :332, :344, :770).
  - The "Your call" prose parser and its five boot repairs.
  - The in-tray report docs the town writes for the manager (wakes.ts).
  - Approving mechanical reports just to acknowledge them.
  - Report docs as the record, in the last step.
- **The inventory, section B, is complete.** It has five tables:
  - every place that writes ask words (all go through `createAsk`, plus planner.ts:183 and secretary.ts:221/261/488);
  - every writer of manager in-tray rows;
  - every reader of rollups;
  - every budget rule (lanes.ts:108-166 `laneBlock` is the one gate);
  - every path that puts a building on a goal (today only `adopt` checks the chain).

  A few minor files are listed as one "unmapped" line.
- **Changes the inventory forced on section C:**
  - A new step 5b: four more in-tray row writers (relay, outbox answer, meeting decisions, mentions).
  - Step 9 is split into 9a (the web reads job threads) and 9b (delete the compatibility layer).
  - Step 4 goes from 350k to 400k.
  - Step 1 goes from 120k to 130k.
- **Cost.** 11 PRs, about **3.31M adjusted tokens**, or **about 3.45M with merges**. The mermaid stretch item adds 50k.
- **Natural stop point after step 5b: about 1.7M.** By then there is one loop and no ceremony approvals, but rollups and the template ask words are still in place.

## What I need from you
Mitchell: read the summary at the top of [dc_uwx045472m](../../note/2026-11/2026-11-10-plan-the-job-abstraction-plan-and-cost-for-mitchel-x045472m.md), then decide whether to build steps 1-5b now (about 1.7M) and decide steps 6-9 at that stop point, or commit to the whole 3.45M. I recommend stopping at 5b first.
