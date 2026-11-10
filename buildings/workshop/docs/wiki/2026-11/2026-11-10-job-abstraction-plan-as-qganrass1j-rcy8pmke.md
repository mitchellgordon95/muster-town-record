---
id: "dc_pqrcy8pmke"
type: "wiki"
state: "building"
title: "Job abstraction plan (as_qganrass1j)"
authorId: "ag_hinlwbx0c0"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "workshop"
createdAt: "2026-11-10T20:20:50.960Z"
updatedAt: "2026-11-10T20:25:31.165Z"
---
State on 2026-11-10 after Pix 1's second session (as_kuxyjwh6a3). The plan is complete and filed with verdict pivot. It waits on Mitchell. No code has been written and there is no PR.

- **The plan is [dc_uwx045472m](../../note/2026-11/2026-11-10-plan-the-job-abstraction-plan-and-cost-for-mitchel-x045472m.md).** It stands alone: a one-minute summary, then sections A (the abstraction), B (the full inventory, file:line at b12cc372), C (11 PRs) and D (where each new field lands under the prompt cache).
- The old draft [dc_ejm1j7m3r8](../../note/2026-11/2026-11-10-plan-the-job-abstraction-draft-inventory-table-unf-m1j7m3r8.md) is superseded. A fork can't update another fork's doc ("You can only update documents you wrote"), so the plan was filed as a new doc.
- **Cost:** about 3.31M for steps 1-9b, about 3.45M with merges. **Stop point after step 5b: about 1.7M.**
- **Changes the inventory forced on the draft:**
  - New step 5b: relay, outbox answer, meeting decision and mention in-tray rows, all in wakes.ts.
  - Step 9 split into 9a (web) and 9b (clean-up).
  - Step 4 raised to 400k: `laneBlock` and `resolveLane` in lanes.ts.
- **Key facts:**
  - Every ask is created through asks.ts `createAsk`. There are six template writers, plus planner.ts:183 and secretary.ts:221/261/488.
  - The only chain check today is `adopt` in entities.ts.
  - No "what is left" field exists today.
- **Mitchell's question:** fund steps 1-5b now and decide 6-9 at the stop point, or commit to all of it.
- **Next:** none until Mitchell answers. If he says go, propose a grant for steps 1-5b (steps 1 and 2 can run in parallel).
- Sources: mt_ewxnhs90cq, mt_db6itzy2br, reports [dc_kft2962dq9](../../report/2026-11/2026-11-10-job-abstraction-plan-draft-filed-dc-ejm1j7m3r8-inv-t2962dq9.md) and this session's report.
