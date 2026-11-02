---
id: "dc_fxj189an5s"
type: "report"
state: "building"
title: "New key result kr_ef11f6ex28 (dead code, flags explicit) per the 1:1; third proposal gr_glon8xr0io (250k, remove the `open` budget mode) in the in-tray; Finn on dead-code sweep 1"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_odhmznuk1x","dc_jfu3h09hks"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-28T19:20:11.965Z"
sessionId: "se_nwc75d5gzk"
createdAt: "2026-10-28T18:09:36.481Z"
updatedAt: "2026-10-28T19:20:11.965Z"
---
## Shipped
Nothing new on main since the last rollup ([dc_wddrnyet2g](2026-10-28-ci-red-on-main-is-untested-pushes-not-flakes-propo-drnyet2g.md)). Live code is unchanged at 41236ee.

## Decided
- [dc_odhmznuk1x](2026-10-28-open-budget-mode-removal-proposed-as-its-own-grant-hmznuk1x.md) (Mara, directed from your town-hall decision 3 via Nell, and 1:1 decision 2 in [dc_fpui0p5b1y](../../meeting-notes/2026-10/2026-10-28-1-1-mitchell-and-mara-notes-ui0p5b1y.md)): approved. Added key result kr_ef11f6ex28 "Unused code paths get found and removed" (sweep report in the cabinet, knip/ts-prune check green in CI on main, at least 3 removals merged; flags covered explicitly with the live value per building and the code behind the other value). Proposed gr_glon8xr0io (250,000 tokens): remove the `open` budget mode, kept as its own proposal rather than folded into gr_8ve21typt6 (different key result). Assigned Finn dead-code sweep 1 (as_xp8fuautz6, exploration, findings only, ~30–40k): knip/ts-prune triage plus a flags section extending Nell's inventory [dc_vie3wrhj54](../../../../bl_vef3v0oux0/docs/note/2026-10/2026-10-28-per-building-flags-where-each-is-set-who-flips-it-e3wrhj54.md) to env/policy/web toggles.
- [dc_jfu3h09hks](2026-10-28-stale-state-drain-flake-1-s-waitfor-timeout-plus-a-u3h09hks.md) (Finn, stale-state flake exploration): approved in the prior session. 0 failures in 50 local runs; cause is a 1 s vi.waitFor timeout (hidden since 07f7957) plus runtime.stop() not awaiting the redeployer's drain. The fix is step 3 of gr_x5gnnmo7yi.

## Key results
- kr_ef11f6ex28 (dead code, NEW, written by me from 1:1 notes [dc_fpui0p5b1y](../../meeting-notes/2026-10/2026-10-28-1-1-mitchell-and-mara-notes-ui0p5b1y.md) and Nell's [dc_vie3wrhj54](../../../../bl_vef3v0oux0/docs/note/2026-10/2026-10-28-per-building-flags-where-each-is-set-who-flips-it-e3wrhj54.md)): not-started. Keep or cut it from this rollup. Proposal gr_glon8xr0io (250k) under it; Finn's sweep 1 running on exploration.
- kr_dctpbbwtno (architecture docs): claimed; gr_z9xj51uox3 closed as done (90,852 / 400,000 spent, remainder returned). Awaiting your met/missed.
- kr_bo4codoha8 (invariants): met by you at 17:32Z.
- kr_oubxzkl4n6 (doc-drift CI): done via PR #58 (+ #62/#63) with no grant; you could mark it met.
- kr_doa59kdway (abstraction sweeps): not-started; proposal gr_8ve21typt6 (260k) open.
- kr_cm5qb2wqh7 (CI green without reruns): not-started; proposal gr_x5gnnmo7yi (150k) open.
- No funded grants right now. Spend today: exploration 172,873 / 828,571 tokens; directed 47,607 tokens (this KR/proposal session).

## Needs from Mitchell
1. Decide the three open proposals in the Town Hall in-tray: gr_8ve21typt6 (260k, abstraction consolidation), gr_x5gnnmo7yi (150k, keep main green: pre-push hook; steps 2 and 3 touch Workshop's v12.test.ts and runtime code, so fund only step 1 if you want a look first), gr_glon8xr0io (250k, remove `open` budget mode; touches core/runtime/web, column stays unread, no migration).
2. Keep or cut kr_ef11f6ex28, and mark kr_dctpbbwtno and kr_oubxzkl4n6 met or missed.

## Key results I wrote (keep or cut: Building → Settings → Key results)
- created kr_ef11f6ex28: "Unused code paths get found and removed: a recurring dead-code sweep (unused exports, unreachable handlers, dead flags, orphaned scripts) lists what nothing calls, incl. for each building/town flag its live value per building and the code only the other value runs; safe removals merged on main." (how to check: A sweep report in the filing cabinet lists candidates with file paths and how each was verified unused (flags: live value per building + the code behind the other value); a dead-code check (knip or ts-prune) runs green in CI on main; at least 3 removals are merged on main.; from [dc_fpui0p5b1y](../../meeting-notes/2026-10/2026-10-28-1-1-mitchell-and-mara-notes-ui0p5b1y.md), [dc_vie3wrhj54](../../../../bl_vef3v0oux0/docs/note/2026-10/2026-10-28-per-building-flags-where-each-is-set-who-flips-it-e3wrhj54.md))
