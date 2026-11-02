---
id: "dc_16g7lkpj46"
type: "report"
state: "building"
title: "Workshop rollup: waterfall steps 1–6 live on bcbab43, step 7b done (c6b9aac); the pilot flip needs Mitchell (Building → Settings → Budget mode, 0059285)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_hab5ns68oa","dc_y9ujqb33om","dc_zmtf9iznsd","dc_qz8k5g3yu5","dc_4dspblhlsa","dc_wwap0nwddl","dc_8du9htnib6","dc_elwkq36to3","dc_lilejk9gg7","dc_ycbpmja2nr","dc_ypirzk9ohn","dc_va9aub6ivi","dc_jd3rl25rgr","dc_3cg618hxp8","dc_ecj706mlug"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-25T14:43:59.059Z"
sessionId: "se_91lrxnm6ur"
createdAt: "2026-10-25T04:58:25.319Z"
updatedAt: "2026-10-25T14:43:59.059Z"
---
## Shipped
All live on **bcbab43** (verified by three live checks, [dc_ypirzk9ohn](2026-10-25-waterfall-step-4-manager-s-1-1-is-live-on-bcbab43-irzk9ohn.md), [dc_va9aub6ivi](2026-10-25-step-6-verified-on-live-bcbab43-contains-40cdeda-r-9aub6ivi.md), [dc_jd3rl25rgr](2026-10-25-step-5-50bd8cc-and-kill-fix-de2fd30-are-live-on-bc-3rl25rgr.md)), unless marked:
- **Waterfall step 3**, Town Hall in-tray (867dc3f, Lena): `intray:town-hall` place, rollups/proposals/checkpoints rows, HUD badge.
- **Step 4**, the manager's 1:1 (c4c1635, Root): meeting kind `one-on-one`, "Talk to ★" on agent and building panels; the route refuses agents (403). Human side tested in core/runtime only, not yet by you.
- **Step 5**, lanes and grants (50bd8cc, Lena): assignment lanes (grant / exploration / directed), `canStart` gate with `heldReason`, 50% / 100% checkpoints that assign the manager a checkpoint rollup, verbs `propose_grant` / `checkpoint_grant`, key-results block in the brief; migration 030.
- **Step 6**, board as the residents' key-results view (40cdeda, Lena); the section appears once a building is goal-directed.
- **Duplicate-session fix** (de2fd30, Root): the desk kill now takes the whole process tree; no double-launched sessions since.
- **Step 7b** (c6b9aac, Root): `AGENTS.md` non-negotiable 1 and the Team line reworded for the waterfall; `docs/waterfall.md` status aligned; town copy [dc_g9d74v8kdb](../../article/2026-10/2026-10-24-design-note-the-waterfall-goal-directed-budgets-re-d74v8kdb.md) synced.
- **Budget mode control** (0059285, Keel, pushed, not yet live): Building panel → Settings → "Budget mode" (open / goal-directed, exploration tokens/day), shown only to holders of `building.fund`. A redeploy was waiting on this session; 0059285 should be live after it.

Live numbers from Keel's check ([dc_jd3rl25rgr](2026-10-25-step-5-50bd8cc-and-kill-fix-de2fd30-are-live-on-bc-3rl25rgr.md)):

| item | value |
|---|---|
| bank inflow | 40,000,000 tokens/day |
| Workshop exploration allowance (10% default) | 4,000,000 tokens/day |
| General pool durableTokens | −708,477 (negative, unexplained) |

## Decided
- [dc_hab5ns68oa](2026-10-24-waterfall-step-3-town-hall-in-tray-in-the-web-push-b5ns68oa.md), [dc_zmtf9iznsd](2026-10-24-town-hall-in-tray-checked-in-the-browser-on-live-b-tf9iznsd.md), [dc_qz8k5g3yu5](2026-10-24-waterfall-step-3-closed-missing-pieces-pushed-to-m-8k5g3yu5.md), [dc_wwap0nwddl](2026-10-24-town-hall-in-tray-badge-verified-on-live-867dc3f-i-ap0nwddl.md) (Lena, step 3 build, browser check, close-out, live badge): approve/continue through to closed on 867dc3f.
- [dc_y9ujqb33om](2026-10-24-step-4-manager-s-1-1-parked-for-the-redeploy-desig-ujqb33om.md) (Root, step 4 plan, parked): approve. [dc_lilejk9gg7](2026-10-25-waterfall-step-4-manager-s-1-1-was-never-pushed-re-lejk9gg7.md) (step 4 on c4c1635): approve, live check assigned. [dc_ypirzk9ohn](2026-10-25-waterfall-step-4-manager-s-1-1-is-live-on-bcbab43-irzk9ohn.md) (live check): approve.
- [dc_4dspblhlsa](2026-10-24-duplicate-step-4-session-put-the-live-session-s-wo-spblhlsa.md) (Root, duplicate-session diagnosis): approve, fix assigned. [dc_elwkq36to3](2026-10-25-duplicate-desk-sessions-after-a-restart-fixed-kill-wkq36to3.md) (fix, de2fd30): approve, live check to Keel.
- [dc_8du9htnib6](2026-10-25-waterfall-step-5-pushed-to-main-50bd8cc-lanes-cans-u9htnib6.md) (Lena, step 5, 50bd8cc): approve; live check to Keel. [dc_ycbpmja2nr](2026-10-25-waterfall-step-6-pushed-to-main-40cdeda-board-key-bpmja2nr.md) (Lena, step 6, 40cdeda): approve. [dc_va9aub6ivi](2026-10-25-step-6-verified-on-live-bcbab43-contains-40cdeda-r-9aub6ivi.md) (live check): approve.
- [dc_jd3rl25rgr](2026-10-25-step-5-50bd8cc-and-kill-fix-de2fd30-are-live-on-bc-3rl25rgr.md) (Keel, step 5 + kill fix live, allowance check): approve; 7a assigned.
- [dc_3cg618hxp8](2026-10-25-step-7b-agents-md-non-negotiable-1-reworded-waterf-g618hxp8.md) (Root, step 7b): approve, done.
- [dc_ecj706mlug](2026-10-25-7a-blocked-on-a-human-agents-can-t-flip-budgetmode-j706mlug.md) (Keel, 7a, parked): approve. He correctly did not work around `building.fund`; his continuation resumes when 0059285 is live and runs the post-flip checks (key-results section on the board, directed assignments still start, no stray `heldReason`), or parks again if the Workshop is still `open`.

## Key results
No funded grant yet: every building is still `budgetMode: open`, so no KR spend to report. After the flip I will file the Workshop's first `propose_grant` (from your 1:1 or my next review session) for you to fund, counter or reject in the Town Hall in-tray.

## Needs from Mitchell
1. **Flip the Town Workshop to goal-directed** (agents can't: `building.fund` is human-only by design). Once 0059285 is live: Building panel → Settings → Budget mode → goal-directed. Or now: `PATCH /api/buildings/workshop` with `{"budgetMode":"goal-directed"}` and your user token. Keel's checks and the first grant proposal wait on this.
2. **Confirm or change the budget defaults** now live in `core/src/policy.ts` BUDGET_POLICY: exploration share 10% of the pool per building (4M tokens/day for the Workshop), directed work bypasses grants, funders = human managers and admins, no grant reservations (ceilings only). Related: the General pool shows durableTokens of −708,477; say if you want that investigated before the flip.
