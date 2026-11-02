---
id: "dc_motiu8tr6k"
type: "report"
state: "building"
title: "Fold \"go fund gr_xxx\" rollups into the grant's in-tray row: PR #265 open, waiting on CI"
authorId: "ag_72lnaghn5v"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_7b4zc7yja3"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/265"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #265 (fold ask-only rollups into the grant/retainer in-tray row) is built with core/server/web tests and docs; the continuation as_xlb168kij9 waits on {pr:265} to merge, redeploy, add the rollup 38 line on dc_7lpbltjy1j and rewrite dc_jcyf86dpdp. Nothing else needed."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-02T03:48:37.020Z"
sessionId: "se_qczrzmddb3"
assignmentId: "as_xawaq7sbvm"
costUsd: 2.9385775999999995
tokens: 146929
turns: 53
createdAt: "2026-11-02T03:48:28.501Z"
updatedAt: "2026-11-02T03:48:37.020Z"
---
## What I did
Built Mitchell's ask from 1:1 mt_7b4zc7yja3: when a rollup only says "go fund gr_xxx", that ask now shows on the grant's own in-tray row instead of as a separate card. It covers core, server and web, with tests in all three and the docs updated. PR https://github.com/mitchellgordon95/muster-town/pull/265 (marked ready). Parked until its CI finishes.

## Findings
- **Core** (`packages/core/src/rollup-asks.ts`): a grant or retainer that waits on a human on its own row now carries `asks`. Those are grant proposals, checkpoints, grants closed as done, and asked retainers. Each ask holds the rollup id, the building, the rollup's own line about the item, and `folded`. An ask counts only from a rollup filed since the item's latest propose/checkpoint/close. The "Already waiting in your in-tray" line the town adds to every rollup is ignored, because it names every open proposal.
- **Submit**: a rollup is folded (acknowledged automatically, decision approve by "system", tag `folded`, a note naming the items) when all of these hold:
  - it names at least one such item,
  - it has no Shipped items,
  - its Needs section says nothing ("Nothing needed.").
  The manager's submit note says it was folded. Checkpoint and close rollups are never folded, because they are their grant's report. A rollup with Shipped items keeps its card.
- **Server/deck**: GET `/api/buildings/town-hall/intray` returns `asks` on grants and retainers. The review deck's proposal, checkpoint, close and retainer slides start with "**Workshop asks you to fund (continue / mark / approve) this:** <line> (rollup dc_…)".
- **Web**: GrantRow and RetainerRow show the ask with a "the rollup →" link. In the deck the slide text carries it, so the row under the slide doesn't repeat it. A pending rollup that keeps its card says "Its ask on gr_x is on that row below."
- **Checks**: `npm run check` passed docs, deadcode and typecheck. In the tests step one timing test failed: server `backup.test.ts`, gap 107 ms against a 100 ms limit, under load. It passed when rerun alone (23/23). The new tests pass: core `rollup-asks.test.ts` (2), server `review-deck.test.ts` (new case), web `rollupAsks.test.tsx` (2). Docs: how-work-gets-done.md §6 has a new bullet, the `submit_report` rollup description is updated, and there is a docs/log.md line.
- **Plan for the continuation**: when PR #265's CI finishes, merge if green and redeploy. Then add a rollup 38 Shipped line to [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md), rewrite topic page [dc_jcyf86dpdp](../../wiki/2026-10/2026-10-28-web-client-panels-and-the-in-tray-yf86dpdp.md) (in-tray rows carry `asks`; ask-only rollups are folded), and check live: the next ask-only rollup should not appear under Manager reports.

## What I need from you
Nothing needed.
