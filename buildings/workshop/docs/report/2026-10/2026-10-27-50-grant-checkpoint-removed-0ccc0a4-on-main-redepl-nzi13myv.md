---
id: "dc_ihnzi13myv"
type: "report"
state: "building"
title: "50% grant checkpoint removed (0ccc0a4 on main); redeploy requested, parked for the live check"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "0ccc0a4 on main; the parked continuation does the live check once CI promotes main to prod (blocked behind Keel's 36a053b run). Nothing more to assign."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T04:35:07.944Z"
sessionId: "se_icdo3rynli"
assignmentId: "as_hc0gwr5efn"
costUsd: 1.1354519
tokens: 63777
turns: 31
createdAt: "2026-10-27T04:09:39.371Z"
updatedAt: "2026-10-27T04:35:07.944Z"
---
## What I did
- Removed the 50% checkpoint and its hold. Committed **0ccc0a4** and pushed it straight to main, then requested a redeploy (image false).
- I'm parked until 0ccc0a4 is live. Then I'll check /api/health and GET /api/grants/gr_jkorz4f49a.

## Findings
- **Code:** `packages/core/src/grants.ts` now sets `CHECKPOINTS = [1]`. The 100% hold and the manager's "Write the checkpoint for …" assignment work as before. The prompt texts (`prompts.ts`, the funded-grant assignment), `budget.ts`/schema comments, `docs/goal-directed-budgets.md`, `docs/waterfall.md`, `docs/wakes.md` and the web mock fixture now say 100% only. No halfway note anywhere.
- **Release:** a new `Grants.releaseHalfway()` runs at World boot. It moves any grant at status checkpoint back to funded when:
  - 1 is not in its `checkpointsDone`, and
  - its spend is under its tokens.
  - It logs history "continue" and a `grant.funded` event "Released from the 50% checkpoint".
  - It is idempotent. If a human already continued or adjusted the grant, it is funded and the release skips it, so both together are harmless.
- **gr_jkorz4f49a is already released:** Mitchell adjusted it to 1,000,000 tokens at 03:58Z. It is funded, spend 153,848, checkpointsDone []. No grant in any building is held at checkpoint right now, so I expect the boot release to release **0 grants**.
- **Fix found along the way:** `checkpoint_grant` used to accept a funded grant only when its `checkpointsDone` was non-empty. A top-up (adjust) clears that list, which is now the only way to continue at 100%, so the manager's checkpoint report would have been refused. It now checks for a "checkpoint" entry in the grant's history instead.
- **Tests:** `core/test/lanes.test.ts` has three new or changed tests:
  - 60% spend creates no checkpoint assignment, and a grant-lane step can start.
  - 100% holds once, then again after a top-up.
  - `releaseHalfway` frees a grant held at 50% and leaves a grant held at 100% alone.
  - Results: core **311/312 pass**, runtime `manage.test.ts` 6/6.
  - The one failure, `v12.test.ts` (duplicate column `origin`), already fails on main without my change. It comes from b4bfdad (Wakes step 1). That commit also leaves 13 web typecheck errors in `mock/fixture.ts` and `mock/sim.ts` (missing `origin`). schema, core, server and runtime typecheck clean. I left these for whoever owns the wakes work.
- Heads-up: Workshop's gr_iq5m7dug56 is at 1,640,037 / 1,666,667 tokens and will hit the 100% checkpoint soon.

## What I need from you
Nothing needed.
