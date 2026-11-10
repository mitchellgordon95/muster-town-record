---
id: "dc_tuuomz93qp"
type: "report"
state: "building"
title: "PR #405 is live and both asks are now clicks, but its boot made two twin asks: PR #406 fixes it and folds 8 twins"
authorId: "ag_0pz3vlng9i"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #405 live and both asks retyped; the twin-ask bug from the boot order is yours to finish in PR #406 (continuation as_j9ev1jk4bc already waits on its CI). After merge, park on its deploy and report the live count: expected 31 open, 8 folded."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-10T00:04:38.230Z"
sessionId: "se_3bzmq724rx"
assignmentId: "as_uywkjilg8q"
costUsd: 1.2082715000000002
tokens: 60414
turns: 26
createdAt: "2026-11-10T00:04:27.523Z"
updatedAt: "2026-11-10T00:04:38.230Z"
---
## What I did
I confirmed dca8e0e9 is live (/api/health, server started 23:55:48Z) and read both asks on GET /api/asks. Both were retyped, but the same boot also created two new duplicate asks. I fixed that in PR #406 (draft): https://github.com/mitchellgordon95/muster-town/pull/406. Typecheck passes and core tests are green (901/901). The new test fails on the old code. I updated the topic page [dc_rdx7am7r9q](../../wiki/2026-11/2026-11-09-grant-titles-and-how-asks-name-a-grant-x7am7r9q.md).

## Findings
- **The retype worked live:**
  - **ak_964oxnm14w** (the repo request) is now a Done / Decline click with no grant attached. Its history has "retyped, was: money on grant gr_30f8obzab8 (Yes / No)".
  - **ak_4nc6kwr1wt** (the key result on code evidence only) is now a Done / Decline click with no target, because kr_4395ff116f already had a live ask.
- **New bug, caused by PR #405:** at boot `backfillAsks` runs before `retypeProseAsks`. The backfill's "already filed" check only looked on the line's new target, so it filed both lines again: **ak_mpfdm8kjj5** (repo, untargeted) and **ak_3nakbll1su** (click on kr_4395ff116f). Mitchell now sees each of those two asks twice.
- **Six older duplicate pairs** come from a boot at 04:47Z on 11-09: the Juno 1:1, Let in on dungeonrpg99-ops, the Optional direct-work line, the directory Pages proof, Step 3 AGENTS.md, and the tell/@mention policy. The Secretary deferred one ask in each pair. In total 39 asks are open, 8 of them duplicates.
- **What PR #406 changes:**
  - A rollup line counts as filed when any ask from that rollup has its title or line, whatever its target or type now.
  - A new boot repair, `foldTwinProseAsks`, folds the live duplicates into one. It keeps the one with a target, else the deferred one, else a ranked one, else the oldest. The others get status folded, with `foldedInto` set and a history entry.
  - The rule is written down as invariant 14 in docs/invariants/asks.md.
- **Expected after deploy:** 8 asks folded and 31 open. ak_964oxnm14w stays and ak_mpfdm8kjj5 folds into it. ak_3nakbll1su (the click on the key result) stays and ak_4nc6kwr1wt folds into it.

## What I need from you
Nothing needed.
