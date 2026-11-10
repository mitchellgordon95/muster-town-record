---
id: "dc_uvmbuifjkp"
type: "report"
state: "building"
title: "Prose asks that only mention a grant become clicks: PR #405 open, waiting on CI"
authorId: "ag_90kxmj8icg"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: PR #405 (proseAskShape: a prose call is money only when it asks for tokens; otherwise policy or a Done/Decline click on the request, captain request, access request or key result it names; boot repair retypeProseAsks). The continuation as_fa7vxob97z is already waiting on PR #405's CI to merge and check ak_964oxnm14w and ak_4nc6kwr1wt live. No redeploy."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-09T23:44:44.138Z"
sessionId: "se_x3defyudtf"
assignmentId: "as_k6p2c0uqxt"
costUsd: 1.1744281999999997
tokens: 58721
turns: 21
createdAt: "2026-11-09T23:44:34.717Z"
updatedAt: "2026-11-09T23:44:44.138Z"
---
## What I did
Changed how asks are read from a rollup's prose (packages/core/src/asks.ts), added a boot repair and tests, and opened draft PR https://github.com/mitchellgordon95/muster-town/pull/405. Typecheck is green and core tests pass (900/900). I did not call redeploy.

## Findings
- **Cause, confirmed live on /api/asks:** both asks are `type: money`, target `grant`, with branches Yes / No.
  - ak_964oxnm14w is on gr_30f8obzab8. Its line names the grant only in "(KR3 of gr_30f8obzab8)".
  - ak_4nc6kwr1wt is on gr_fibsfwr4tz, which is named only in its item title. Its line asks Mitchell to flip kr_4395ff116f to missed.
- **The bigger risk:** asks fold by target, whatever their type. Keeping a click on its grant would not be enough, because `fileGateAsk` turns any live ask on that grant into the Adjust / Cut gate. So a click that merely mentions a grant is no longer filed on the grant.
- **New rule, `proseAskShape`:** a call becomes a money ask only when it asks for tokens. That means a verb such as fund, counter, reject, adjust, cut, continue, raise, top up, stop, close, approve or ceiling, or a figure like "150k" or "200,000 tokens". Anything else is:
  - a policy ask, if it vetoes a rule (that rule is unchanged), or
  - a Done / Decline click, filed on the request, captain request, access request or key result it names, otherwise untargeted.
  - Stop and close are on the list so the existing test where a grant decision retires its ask still passes.
- **Boot repair, `retypeProseAsks`** (runs at boot in world.ts, after `retitleProseAsks`):
  - It retypes live prose-read money asks whose line asks for no tokens.
  - It keeps each ask's id, title, body, sources, rank and status, re-checks it as a click, and records a "retyped" entry giving the old type and target.
  - If the new target already has a live ask, the retyped ask stays untargeted, so no target gets two rows.
  - Running it twice changes nothing, and the backfill files no duplicate.
- **Tests** are in prose-ask-titles.test.ts:
  - The repo line files untargeted and the key-result line files on its key result, both as clicks.
  - "Continue gr_x at its gate or cut it" stays money and joins the proposal's own ask.
  - The repair retypes exactly 2 asks and leaves the token call alone.
- The rule is written up as invariant 13 in docs/invariants/asks.md, and topic page [dc_rdx7am7r9q](../../wiki/2026-11/2026-11-09-grant-titles-and-how-asks-name-a-grant-x7am7r9q.md) is updated.
- **What Mitchell should see after the deploy (not yet checked live):**
  - ak_964oxnm14w becomes a Done / Decline click with no grant attached, so it stops showing as a funding question in the "Any collective publishes its docs to GitHub" row.
  - ak_4nc6kwr1wt becomes a Done / Decline click on its key result, or untargeted if that key result already has a live ask.

## What I need from you
Nothing needed. I resume when PR #405's CI finishes, then merge it and check both asks live.
