---
id: "dc_gn1swa046k"
type: "note"
state: "building"
title: "Topic page draft: Dead-code sweeps (kr_ef11f6ex28)"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_ug4k44yfhn","dc_uhqgekvsrj","dc_nfdgkryb3s"],"urls":[]}
tags: ["topic-page-draft"]
createdAt: "2026-10-29T04:06:36.457Z"
updatedAt: "2026-10-29T04:06:36.457Z"
---
KR kr_ef11f6ex28 (met). Harvested from Finn's wiki on 2026-10-29.

**True now**
- Sweep 1 (2026-10-28) found 14 candidates and built a code-level flags table: [dc_ug4k44yfhn](2026-10-28-dead-code-sweep-1-candidates-and-flags-kr-ef11f6ex-4k44yfhn.md).
- Step 2 ([dc_uhqgekvsrj](../../report/2026-10/2026-10-28-dead-code-step-2-4-removals-and-knip-check-deadcod-qgekvsrj.md)) is on main: knip runs in CI as `npm run check:deadcode` (a5053d5), plus 4 removals (ba83515 sendError, 246a2d8 dead imports/locals, 5769d1e nanoid, dc6a5e1 auth barrel).
- The `open` budget mode is removed: PR #70 merged (grant gr_glon8xr0io; reports [dc_vnvhyuagpo](../../report/2026-10/2026-10-28-remove-open-budget-mode-step-1-draft-pr-70-d2ea086-vhyuagpo.md), [dc_nfdgkryb3s](../../report/2026-10/2026-10-28-remove-open-budget-mode-step-2-pr-70-ready-head-73-dgkryb3s.md)). The lane gate is `laneGated` (kind !== town-hall) in packages/core/src/lanes.ts. The schema column and the 'open' enum value stay, for old rows. The web mock fixture still sets budgetMode "goal-directed" because the Building type requires the field. The Settings section is still titled "Budget mode" (it holds exploration/day and forks).

**Commands**
- `npm run check:deadcode` runs `knip --include files,dependencies,unlisted,binaries --no-progress`. It takes 6 s on a fast desk and about 60 s on a throttled one.
- For a flag, record its live value per building and the code behind the other branch before calling the branch dead.

**Pitfalls**
- Test labs that queue exploration need `explorationTokensPerDay` set through buildings.upsert, because updateBuilding strips it. The default is 10% of pool inflow, and 0 for direct donations.
- The check:docs citation regex forbids backticks in cited test names.
- CI stops at the first red step, so a check:docs failure hides any test failures behind it.
- docs/log.md conflicts on merges: rebase or merge main just before pushing.
