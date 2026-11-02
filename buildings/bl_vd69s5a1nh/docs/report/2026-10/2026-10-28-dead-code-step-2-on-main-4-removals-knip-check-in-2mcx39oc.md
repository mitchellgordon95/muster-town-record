---
id: "dc_2o2mcx39oc"
type: "report"
state: "building"
title: "Dead-code step 2 on main (4 removals + knip check in CI, 54b4d02); gr_glon8xr0io step 1 started; we lack town.redeploy"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_uhqgekvsrj"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-28T23:16:50.597Z"
sessionId: "se_dli0anyc5z"
createdAt: "2026-10-28T20:06:12.537Z"
updatedAt: "2026-10-28T23:16:50.597Z"
---
## Shipped
On main, not yet live (Finn, report [dc_uhqgekvsrj](2026-10-28-dead-code-step-2-4-removals-and-knip-check-deadcod-qgekvsrj.md)), one commit per item so each reverts alone:
- `sendError` removed 0bb9a39; 4 dead imports/locals 294031f; `nanoid` dropped from server and runtime fb090bf; 5 auth-barrel re-exports ebbef6d.
- knip dead-code check in CI: knip.json + `npm run check:deadcode`, run right after check:docs, 576fa3d; README 54b4d02.
- CI run 40759124041 (attempt 1): check:docs, check:deadcode, typecheck green. `npm test` red only because Pix's 689761f (landed just before) pushed docs/manual.md over its 1,900-word cap (manual.test.ts). Workshop's doc; Finn told Pix. Nothing of ours is red.
- Candidates note [dc_ug4k44yfhn](../../note/2026-10/2026-10-28-dead-code-sweep-1-candidates-and-flags-kr-ef11f6ex-4k44yfhn.md) updated with the commits; `tsc --noUnusedLocals` finds nothing in desk/cli/core src.

## Decided
- [dc_uhqgekvsrj](2026-10-28-dead-code-step-2-4-removals-and-knip-check-deadcod-qgekvsrj.md) (Finn, dead-code step 2) → approve. Done as scoped.
- Finn's grant step 1 for gr_glon8xr0io (as_pg5q3cgkda: core + schema + tests for removing the `open` budget mode) was queued behind this and is now unblocked.
- Asked Nell to queue the redeploy for 54b4d02 once main is green (the redeploy tool refuses both Finn and me).

## Key results
- kr_ef11f6ex28 (dead code), grant gr_glon8xr0io: 30,198 / 250,000 tokens. Status not-started until step 1 reports. Its check (sweep report in the cabinet, ≥3 removals merged, knip green in CI on main) is met by today's commits once main is green; the `open` removal is the grant's remaining work.
- kr_doa59kdway (abstraction sweeps): proposal gr_8ve21typt6 (260k) still open in your in-tray.
- kr_cm5qb2wqh7 (CI green on attempt 1): proposal gr_x5gnnmo7yi (150k) still open. Today's red (manual.md cap) is the same pattern Finn's root cause found: an untested direct push, not a flake.
- kr_oubxzkl4n6 (doc-drift CI) is done (PR #58, #62, #63) and never had a grant; you could mark it met.
- Spend by lane today: exploration 353,627 / 828,571 tokens; directed 47,607 tokens.

## Needs from Mitchell
1. Give this building (Mara, ag_croreod6q3) the town.redeploy permission: the town rule says to queue a redeploy when work lands, but the tool refuses us, so each deploy goes through Nell.
2. FYI only: main is red from Pix's 689761f (manual.md 1,924 words vs the 1,900 cap). Pix has been told; no action unless it stays red.
