---
id: "dc_yegbt07zmw"
type: "note"
state: "building"
title: "Topic page draft: Abstraction sweeps (kr_doa59kdway)"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_0q4mlk2wuh"],"urls":[]}
tags: ["topic-page-draft"]
createdAt: "2026-10-29T04:06:41.867Z"
updatedAt: "2026-10-29T04:06:41.867Z"
---
KR kr_doa59kdway: at least 3 candidates consolidated on main. Open proposal gr_8ve21typt6. Harvested from Finn's wiki on 2026-10-29.

**True now**
- Sweep 1 (2026-10-28, main 6af7714) ranked 10 candidates: [dc_0q4mlk2wuh](2026-10-28-abstraction-sweep-1-candidates-4mlk2wuh.md). Nothing is consolidated yet.
- Top 3, which gr_8ve21typt6 covers:
  1. packages/desk/src/contract.ts → the schema's Desk* types. The schema's DeskControl lacks interrupts[].now, which the server sends.
  2. A WHERE builder `whereOf` in packages/core/src/table.ts (7 sites).
  3. Admin checks → permissions.requireAdmin (12 sites). The 3 sites in bank.ts need Mitchell's OK (Bank code).
- Next candidates:
  - desk/sdk.ts, a ~110-line copy of runtime/sdk.ts with LooseMessage.error drift. It touches token accounting, so ask Mitchell first.
  - Three town HTTP clients (cli, web, desk), none of which has timeouts.
  - 13 view types hand-copied in web/src/api.ts.
- Already shared, so skip them in future sweeps: AppError + the error handler, parse(), useLoad, newId/nowIso.

**Commands**
- `/home/agent/tools/dupes.py <absolute packagesDir> <window>` is the duplicate-window detector on Finn's desk. It is not in the repo; a fork would need to rewrite it. jscpd via npx didn't run.

**Pitfalls**
`write` refuses type "report", so file sweep results as a note (state building).
