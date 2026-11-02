---
id: "dc_wddrnyet2g"
type: "report"
state: "building"
title: "CI red on main is untested pushes, not flakes: proposal gr_x5gnnmo7yi (150k) filed for kr_cm5qb2wqh7; one repo setting needed"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_bp0drrs0ao"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"1:1: Mitchell and Mara\": Mara: add key result \"Unused code paths get found and removed\" (dead-code sweep report, knip/ts-prune check green in CI on main, >=3 removals merged) to the bui"
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-28T17:53:37.276Z"
sessionId: "se_1n6miaxfce"
createdAt: "2026-10-28T17:45:34.322Z"
updatedAt: "2026-10-28T17:53:37.276Z"
---
## Shipped
Nothing on main this round. Finn's findings note [dc_l59kklky3v](../../note/2026-10/2026-10-28-ci-red-on-main-last-20-runs-and-the-v12-desk-slots-9kklky3v.md) (filing cabinet): the last 45 main runs with the cause of every red one, and the v12 desk_slots root cause reproduced locally (3 of 3 fail without the undo line, 3 of 3 pass with it).

## Decided
- [dc_bp0drrs0ao](2026-10-28-ci-red-on-main-is-untested-pushes-not-flakes-v12-d-0drrs0ao.md) (Finn, CI root cause) → approved. None of the last 200 main runs was retried, so there are no flakes to fix. 4 of the last 20 main runs were red; every one was a deterministic break pushed untested straight to main (duplicate `isManager`, manual.md over its word cap twice, the desk_slots undo line, two migrations numbered 050) and each was fixed by a follow-up commit. 4 of those 5 episodes were Root's direct pushes from Workshop. The desk_slots failure is structural: v12.test.ts undoes every later migration by hand, so each new table-adding migration breaks it until someone adds the undo line.
- Filed proposal gr_x5gnnmo7yi (150,000 tokens) for kr_cm5qb2wqh7: a pre-push hook (check:docs, typecheck, test) installed on every desk by npm prepare; v12.test.ts rebuilt forward from migrations 001–004 so new migrations can't break it; the one open flake (run 40454959781, runtime stale-state drain test) fixed at the root. Stop: 20 consecutive main runs green on attempt 1.
- Assigned Finn exploration as_u9ec6c7okc: reproduce that stale-state flake, findings only, ~30k.

## Key results
- kr_cm5qb2wqh7 (CI green without reruns): not-started; proposal gr_x5gnnmo7yi open. Currently 4 of the last 20 main runs red, none retried.
- kr_doa59kdway (abstraction sweeps): not-started; proposal gr_8ve21typt6 (260k) still open, independent of this one.
- kr_dctpbbwtno (architecture docs): claimed, close rollup [dc_nqahc0xwbk](2026-10-28-architecture-docs-grant-gr-z9xj51uox3-closed-as-do-ahc0xwbk.md) awaiting your met/missed.
- kr_bo4codoha8 (invariants): met. kr_oubxzkl4n6 (doc-drift CI): done on main (PR #58), never marked met.
- No funded grant open. Spend today by lane: exploration 90,479 / 828,571 tokens, directed 0 tokens.

## Needs from Mitchell
1. Decide gr_x5gnnmo7yi, and say whether we may edit packages/core/test/v12.test.ts (Workshop's test, last fixed by Lena in d4fccbb) or whether Workshop rewrites it; without step 2 the ask drops to ~80k.
2. Set the GitHub repo rule "require branches to be up to date before merging" on main: it stops two PRs each adding a migration 050 from merging on top of each other (the #65 episode). Only a repo admin can set it.
