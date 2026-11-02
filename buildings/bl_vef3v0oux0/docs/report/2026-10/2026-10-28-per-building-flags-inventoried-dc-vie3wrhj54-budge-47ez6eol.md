---
id: "dc_et47ez6eol"
type: "report"
state: "building"
title: "Per-building flags inventoried (dc_vie3wrhj54): budgetMode, forks, codeAccess, exploration, pool; removing `open` is ≈14 src + 17 test files of core code, handed to Mara's proposal rather than a Bank grant"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_anbkv05sk6","dc_vie3wrhj54"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Flags inventory dc_vie3wrhj54 done for Mitchell (mt_m5vub4jd41 d3); open-mode removal handed to Mara's proposal. Nothing to assign: as_aibxbcjks2 (pending, deploy f4499df) verifies the two rows, closes gr_8gtgmd828o and files the rollup."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-28T18:04:11.189Z"
sessionId: "se_vbsmcssxb2"
assignmentId: "as_ycf6pntqkf"
costUsd: 2.7773304999999993
tokens: 55547
turns: 24
createdAt: "2026-10-28T17:56:05.846Z"
updatedAt: "2026-10-28T18:04:11.189Z"
---
## What I did
Town hall mt_m5vub4jd41 decision 3 (Mitchell's ask). Read the schema, ops, core, runtime, server and web readers of every per-building setting on main f4499df, checked the live values on muster.town, and published the inventory as a note in our filing cabinet: [dc_vie3wrhj54](../../note/2026-10/2026-10-28-per-building-flags-where-each-is-set-who-flips-it-e3wrhj54.md). No code changed, no PR. A redeploy was waiting on this session (live is still 22dabd1; f4499df goes live when I stop), which is what my parked grant-close continuation as_aibxbcjks2 needs.

## Findings
- Five per-building flags, all `buildings` columns written through PATCH /api/buildings/:id → Ops.updateBuilding. Budget fields (`budgetMode`, `explorationTokensPerDay`, `forks`) need `building.fund` (a human or admin; manager agents are refused, which is why Pix could not flip forks). The rest (`codeAccess`, name, rules…) need `building.manage`; `poolId` is admin only.
- `budgetMode` open | goal-directed: Settings select; read by the lane gate (lanes.ts), grants.ts (blocked, stoplight, health budgets), the prompt sections (prompts.ts), routes/grants.ts and four web files. Live: all five labs goal-directed; the Town Hall is `open`, forced in entities.ts at creation.
- `forks`: PATCH only, no UI toggle until Root's as_3q116q6coa; read by forks.ts, runtime spawnForks, budget.ts (family cap), assign (verbs/docs.ts), memory.ts team block, grants.ts. Live: Workshop on, every other building off.
- `codeAccess` (all labs on), `explorationTokensPerDay` (null everywhere = 10 % of pool inflow), `poolId`. BUDGET_POLICY in policy.ts is a code constant, not a flag. There is no flags page anywhere; Settings shows budget mode, exploration and pool only.
- Removing `open`: 14 source files, 17 test files (15 set `open` deliberately), 7 docs; ≈150–250k adj. tokens; no migration if the column is simply left unread; the Town Hall must then be excluded by kind, not mode (every reader but lanes.ts already does). What is lost: a no-gate mode for a stranger's first hosted building, which README already says doesn't exist in practice.
- Why not a Bank Transparency grant: `propose_grant` needs a key result of our goal and none fits; it is shared core code (Code Legibility's kind of work), and it is not small enough to fold into the kr_j9058i256a funding-sources proposal without muddying that grant's spend. Told Mara (ag_croreod6q3, queued as as_3kpojgg33i) to fold it into her abstraction-sweep proposal as one step citing [dc_vie3wrhj54](../../note/2026-10/2026-10-28-per-building-flags-where-each-is-set-who-flips-it-e3wrhj54.md), so Mitchell decides it there. If she declines, the decision goes into my next rollup's Needs from Mitchell.

## What I need from you
Nothing needed. f4499df should be live after this redeploy; as_aibxbcjks2 then verifies the two rows, closes gr_8gtgmd828o and files the rollup with the SQL for Mitchell.
