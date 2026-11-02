---
id: "dc_ujc1l2z1mh"
type: "report"
state: "building"
title: "Town Hall draws from the Bank like any building (PR #137, 1d7b852); live check parked"
authorId: "ag_sfp9m53cw2"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #137 (1d7b852) merged under Mitchell's Bank yes from 1:1 mt_cz11aqe81a; the live check already waits on deploy 1d7b852 (as_g5h18xqiym) and step 7 (as_3xd2xv78h1) starts when this assignment finishes. Rollup 34 will carry it as a Shipped item with the \"Plan with an agent needs a signed-in human\" note in Your call."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T01:37:32.460Z"
sessionId: "se_3u62019btd"
assignmentId: "as_xl8nklxh62"
costUsd: 2.8443695
tokens: 142218
turns: 70
createdAt: "2026-10-31T01:37:23.174Z"
updatedAt: "2026-10-31T01:37:32.460Z"
---
## What I did
Removed the Town Hall special case from the Bank (1:1 mt_cz11aqe81a, Mitchell's "go ahead" counts as the Bank ask-first yes under [dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-10-30-schema-mi-qoh7ppen.md)). Merged PR https://github.com/mitchellgordon95/muster-town/pull/137 as **1d7b852** (local `npm run check` and CI both passed). Queued the redeploy. Rewrote the topic pages [dc_0xqyrevla1](../../wiki/2026-10/2026-10-30-town-level-goal-tree-design-qyrevla1.md) and [dc_rke20gvrqr](../../wiki/2026-10/2026-10-28-bank-and-token-accounting-e20gvrqr.md). The live check is parked until deploy 1d7b852.

## Findings
- **Core `bank.ts`:** `drawPool` now returns the building's pool (`poolOf`) for any known building. `shares()` gives an auto share to any pool that has a building. The Bank summary's per-building `pct` is now the pool's share for every building. The Town Hall sits in General, so it shares General first come, first served, like the Workshop.
- **Planner (`goal-changes.ts`):** `canRun` goes through `Budget.canStart` as before, and the Town Hall now has a share, so the Planner can start. `PLANNER_UNPAID` is reworded and only posts when the Bank can't fund the Town Hall (no credential, its share used up, or its daily cap reached). The reorg meeting is facilitated by the Planner when it can run.
- **Runtime `session.ts`:** removed the special path that recorded Town Hall usage without debiting the Bank. This affects more than the Planner: librarian (Ada) chats and any other Town Hall host session now debit General too.
- **Finance and web:** every building is marked `drawsFromBank`. The Town Hall's exploration allowance is still 0, from `Grants.exploration`. The Bank pools table, the building panel's pool picker and the map's pool flows and legend now include the Town Hall. The mock follows.
- **Tests:**
  - New core test (goals-step5): with a credited Bank, the Town Hall has the same `available` as the Workshop-like lab. The Planner opens with no notice, a 400-token Planner charge lowers the Town Hall's pool by 400, and the Planner facilitates the reorg meeting.
  - Updated to the new rule: bank.test, finance-pools.test, running-debit.test and the librarian chat test, plus docs/invariants/bank.md invariant 7.
  - All other existing tests pass unchanged.
- No migration. Docs updated: goals.md step 5, architecture.md, log.md.
- **Live check still to do:** commit 1d7b852 should be live after the redeploy. Next session:
  - Confirm GET /api/health shows a commit containing 1d7b852.
  - Confirm GET /api/bank lists the Town Hall with General's pct and a non-zero balance.
  - "Plan with an agent" needs a signed-in human, so a guest can't open it. That goes in rollup 34's "Your call" line.

## What I need from you
Nothing needed.
