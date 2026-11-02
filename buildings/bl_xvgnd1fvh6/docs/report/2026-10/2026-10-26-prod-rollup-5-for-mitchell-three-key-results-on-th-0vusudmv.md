---
id: "dc_ix0vusudmv"
type: "report"
state: "building"
title: "Prod rollup #5 for Mitchell: three key results on the board, stress-test grant gr_wqnunw5yd8 filed throwaway-first; two things only you can decide"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_jc8cgovfos"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-26T16:14:46.691Z"
sessionId: "se_dfr4p13zbl"
createdAt: "2026-10-26T15:52:15.068Z"
updatedAt: "2026-10-26T16:14:46.691Z"
---
## Shipped
- Prod's three key results are live on the board (written with `set_key_result` on 7ebf5ab, verified on `GET /api/buildings/bl_xvgnd1fvh6`): kr_z9lcfnvt94 load test on a throwaway clone, kr_giqd28iwcb off-site backup + one restore drill, kr_wm6mphmrjf Mac-issued token rotation. Stoplight went from "no key results" to red "no funded grant on any of its 3 key results".
- Grant proposal **gr_wqnunw5yd8** filed against kr_z9lcfnvt94, throwaway-first as you asked on rollup #3: a second Fly app `muster-town-stress` (same image and size, fresh state, no live secrets, desks off), WebSocket ramp 10 → 400 viewers and scripted-agent ramp 5 → 80, Bottleneck 1 and 2 reproduced twice. The only production change is a read-only `load` block on `/api/health`; the harness refuses a muster.town URL. Full write-up: [dc_x4twxh1a8o](../../note/2026-10/2026-10-26-stress-test-grant-the-proposal-as-filed-throwaway-twxh1a8o.md). Ask 10 M tokens (≈ $15) plus under $5 of Fly.

## Decided
- [dc_jc8cgovfos](2026-10-26-stress-test-grant-filed-throwaway-first-gr-wqnunw5-8cgovfos.md) (Cleo, stop) → approve. Finished work; its two asks are below.
- Started one exploration on kr_giqd28iwcb (as_qiry4n1avf, me, under 1.5 M tokens of today's allowance): compare three backup destinations for town.db (Wright's VPS over rsync, a Fly Tigris bucket, a GitHub private repo), address WAL-safe copies, and draft the backup grant so it can be filed the moment gr_wqnunw5yd8 is decided. No production change, no secret, no grant filed.
- Two pending assignments are moot and will just report that: as_kxtf3y8y07 (KRs already written) and as_iv8fk97gf8 (grant already filed).

## Key results
- No funded grant yet, so no grant spend. Exploration today: 0 of 5.4 M tokens before as_qiry4n1avf.
- kr_z9lcfnvt94: not-started, proposal gr_wqnunw5yd8 open.
- kr_giqd28iwcb: not-started, exploration running.
- kr_wm6mphmrjf: not-started, waits for its turn (one open proposal per building).

## Needs from Mitchell
1. Fund, counter or reject gr_wqnunw5yd8 in the Town Hall in-tray, and pick the Fly access: (a) you create app `muster-town-stress` plus a deploy token for it, stored as Town Hall secret `FLY_STRESS_TOKEN` granted to the grant, or (b) you run `deploy/fly/throwaway.sh` at the start and `--destroy` at the end. The real FLY_API_TOKEN never goes on the throwaway.
2. Keep or cut the three key results listed below this rollup; the backup grant will be drafted against kr_giqd28iwcb as worded.

## Key results I wrote (keep or cut: Building → Settings → Key results)
- created kr_z9lcfnvt94: "A load test on a throwaway clone of the town Machine (Fly shared-cpu-2x / 2 GB) reports the max concurrent viewers and agents it sustains and names the first two bottlenecks with the measurement behind each; no load is ever sent to muster.town." (how to check: Prod's filing cabinet has the grant's checkpoint report with one row per ramp step, a ceiling line per load, and Bottleneck 1 and 2 sections citing two runs and a file; scripts/stress/ is on main; the throwaway app is deleted at the end; muster.town health stayed ok throughout.; from [dc_qg2gppz9jd](../../../../../library/meeting-notes/2026-10/2026-10-26-town-hall-town-hall-notes-2gppz9jd.md), [dc_uvd6q8bbh6](2026-10-26-prod-rollup-3-for-mitchell-stoplight-live-pr-56-st-d6q8bbh6.md), [dc_5u5a14j32z](2026-10-26-prod-rollup-4-for-mitchell-three-key-results-draft-5a14j32z.md))
- created kr_giqd28iwcb: "The live world has an off-site backup: a copy of town.db leaves the Fly volume at least nightly, and one restore from it onto a scratch Machine has been done and written up." (how to check: deploy/README.md names the backup destination and the restore steps; GET https://muster.town/api/health shows backup.lastAt under 24 h old; a Prod report shows the restore drill with the restored town's agent and doc counts matching production.; from [dc_5u5a14j32z](2026-10-26-prod-rollup-4-for-mitchell-three-key-results-draft-5a14j32z.md))
- created kr_wm6mphmrjf: "Every admin and agent token in the live database was issued after the move to Fly: the Mac-issued ones are revoked, and the rotation procedure is in docs/secrets.md." (how to check: docs/secrets.md has a Rotate section; the old Mac-issued admin token gets 401 from https://muster.town/api/me; a Prod report lists each rotated token kind with the date.; from [dc_5u5a14j32z](2026-10-26-prod-rollup-4-for-mitchell-three-key-results-draft-5a14j32z.md))
