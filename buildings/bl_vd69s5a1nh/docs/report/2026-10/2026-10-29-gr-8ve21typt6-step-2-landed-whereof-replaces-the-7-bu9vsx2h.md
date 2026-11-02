---
id: "dc_mkbu9vsx2h"
type: "report"
state: "building"
title: "gr_8ve21typt6 step 2 landed: whereOf() replaces the 7 hand-rolled WHERE builders (PR #88 → 267c2ed, PR and main CI green on attempt 1, redeploy called)"
authorId: "ag_ms2bbuihlr"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_0q4mlk2wuh","dc_xa94tbls1r","dc_fwhnaxcfsx"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/88","https://github.com/mitchellgordon95/muster-town/actions/runs/40952633120","https://github.com/mitchellgordon95/muster-town/actions/runs/40952946202"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: whereOf() in core/src/table.ts, 7 sites replaced, PR #88 → 267c2ed, PR and main CI green on attempt 1, 6 unit tests. Step 3 (as_eee4uhqme7, requireAdmin) is released by this; close_grant + the single rollup follow when it lands."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-29T20:56:18.300Z"
sessionId: "se_su445ul2j8"
assignmentId: "as_ytk34rczmr"
costUsd: 0.9660942000000003
tokens: 48305
turns: 22
createdAt: "2026-10-29T20:56:09.955Z"
updatedAt: "2026-10-29T20:56:18.300Z"
---
## What I did
I added `whereOf()` to packages/core/src/table.ts and used it in all 7 places that built their own WHERE clauses. I tested it, merged PR https://github.com/mitchellgordon95/muster-town/pull/88 myself after its CI passed, and called `redeploy`. I also filed note [dc_fwhnaxcfsx](../../note/2026-10/2026-10-29-gr-8ve21typt6-step-2-landed-whereof-hnaxcfsx.md) (tagged kr_doa59kdway) and updated the "Abstraction sweeps" topic page [dc_xa94tbls1r](../../wiki/2026-10/2026-10-29-abstraction-sweeps-94tbls1r.md).

## Findings
- **Merge commit: 267c2ed** (267c2edeff51fe7dc7e340c339c0b6b18a995740). It should be live after the redeploy I called; I haven't checked that it is.
- **CI:** the PR run 40952633120 passed on attempt 1 (check took 2m01s). The main run 40952946202 passed on attempt 1 (check and promote).
- **What `whereOf(conds, extra)` does:**
  - Each filter that is set becomes `col = ?`, or `col IN (?, …)` for an array.
  - Filters that are undefined, null or "" are skipped. This matches the old `if (x)` checks.
  - An empty array becomes `0 = 1`, which matches nothing.
  - Hand-written SQL pieces go in `extra`, each with its own params, so the params stay in line with their `?`s. Entries that are false or empty are skipped.
  - Everything is joined with AND. If nothing applies it returns "", and `Table.where` treats "" as every row.
  - It is exported from @muster-town/core. There are 6 unit tests in packages/core/test/table-where.test.ts (no conditions, one, unset ones skipped, array → IN, extra pieces, a bad column name rejected).
- **The 7 sites replaced:**
  1. core/src/events.ts `list()`
  2. core/src/grants.ts `list()`
  3. core/src/skills.ts `visibleTo()`
  4. core/src/verbs/docs.ts `cabinetDocs()`
  5. core/src/verbs/docs.ts `searchDocs()`
  6. server/src/routes/docs.ts GET /api/docs
  7. server/src/routes/docs.ts GET /api/meetings
- **Behaviour:** the queries match the same rows as before. The conditions now come in a different order in the SQL, which doesn't change results under AND. LIMIT handling is unchanged. In `cabinetDocs`, `buildingId` stays in the hand-written SQL on purpose: as a normal filter, an empty building id would be skipped and the cabinet would show every building's docs.
- **Checks on my desk:** `grep -rn "where.push" packages/core/src packages/server/src/routes/docs.ts` finds nothing. `npm run typecheck`, core tests (77 files, 464 tests), server tests (25 files, 133 tests) and `npm run check:docs` all pass. core/src/bank.ts is untouched.
- **Grant progress:** 2 of 3 steps are merged (d30bfdd, 267c2ed). Step 3 (as_eee4uhqme7, requireAdmin) can start now.

## What I need from you
Nothing needed.
