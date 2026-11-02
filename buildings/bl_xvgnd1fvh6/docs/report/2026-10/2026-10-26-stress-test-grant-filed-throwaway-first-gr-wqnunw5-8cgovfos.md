---
id: "dc_jc8cgovfos"
type: "report"
state: "building"
title: "Stress-test grant filed throwaway-first (gr_wqnunw5yd8) against Prod's new key result; all three Prod key results written as Mitchell asked"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_uvd6q8bbh6","dc_5u5a14j32z","dc_x4twxh1a8o","dc_qg2gppz9jd"],"urls":["https://muster.town/api/buildings/bl_xvgnd1fvh6","https://muster.town/api/health"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done: three KRs live on the board, gr_wqnunw5yd8 filed throwaway-first. The Fly-access choice and the funding decision go to Mitchell in rollup #5."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-26T15:51:35.830Z"
sessionId: "se_agjyn15zad"
assignmentId: "as_rl94u7cd5z"
costUsd: 2.75632085
tokens: 26467
turns: 23
createdAt: "2026-10-26T15:51:03.510Z"
updatedAt: "2026-10-26T15:51:35.830Z"
---
## What I did
Mitchell replied on rollup #3 ([dc_uvd6q8bbh6](2026-10-26-prod-rollup-3-for-mitchell-stoplight-live-pr-56-st-d6q8bbh6.md)): "let's do load testing on a throwaway first, i don't want to break stuff that's running", and on rollup #4 ([dc_5u5a14j32z](2026-10-26-prod-rollup-4-for-mitchell-three-key-results-draft-5a14j32z.md)): "you can now write key results yourself, please do" (7ebf5ab is live, so `set_key_result` works for me). Both replies feed the same deliverable, so I did both here:
1. Wrote Prod's three key results from rollup #4 with `set_key_result`, the stress-test one reworded to the throwaway: kr_z9lcfnvt94 (load test on a throwaway clone, no load ever on muster.town), kr_giqd28iwcb (off-site backup + restore drill), kr_wm6mphmrjf (Mac-issued token rotation). Verified on the live API: 3 key results, stoplight red "no funded grant on any of its 3 key results" (was "no key results to work toward").
2. Rewrote the draft [dc_x4twxh1a8o](../../note/2026-10/2026-10-26-stress-test-grant-the-proposal-as-filed-throwaway-twxh1a8o.md) to throwaway-first and filed it: **gr_wqnunw5yd8**, status proposed, in the Town Hall in-tray for Mitchell to fund, counter or reject.

## Findings
- **The plan now sends no load to production.** A second Fly app `muster-town-stress` (same image and size, shared-cpu-2x / 2 GB, iad, own volume) boots fresh: no copy of the live state, none of the live secrets, desks off (maxRunning 0, no FLY_API_TOKEN, no Claude token), so it can neither start Machines nor spend tokens. The harness fills it to live scale (13+ bodies, comparable docs; its `/api/town` snapshot is compared to live's 26 KB) and is deleted at the end. The only production change is a read-only `load: {lagMs, rssMb, wsClients}` on `/api/health`, shipped through CI; the harness refuses a muster.town URL (testing-plan line 4).
- **What the grant measures:** max concurrent viewers (WebSocket ramp 10 → 400) and max scripted agents (verb ramp 5 → 80), each with the failure signal that set it, and Bottleneck 1 and 2 reproduced twice with the code path. Candidates from the code: per-client JSON.stringify fanout on one thread (packages/server/src/ws.ts), synchronous SQLite writes per tile step, the 2 GB Machine.
- **What it does not measure:** the desk-side ceiling (Fly Machine starts, 1.5 s polling per session, Claude org limits) needs real desks, which the throwaway deliberately lacks; the report ranks it from the code and the 2026-10-25 limit death and prices a follow-up (a throwaway desks app).
- **Cost:** ask 10 M tokens (≈ $15 at my blended $1.54 / M); Fly extra about $0.02 / h for the Machine (under $3 if it lives a week) plus a 10 GB volume ($1.50 / mo), both destroyed with the app.
- **Fly access is the one gap:** a desk cannot create apps. The proposal's note offers (a) Mitchell creates `muster-town-stress` and a deploy token for it, stored as a Town Hall secret `FLY_STRESS_TOKEN` granted to the grant (like MINICLAW_* for the Wright skill), after which the grant needs nothing more; or (b) he runs `deploy/fly/throwaway.sh` at the start and `--destroy` at the end. The real FLY_API_TOKEN (muster-desks deploy token) never goes on the throwaway.
- Two assignments are now moot and will just report that when they run: as_kxtf3y8y07 (reply on rollup #4: the key results are written) and as_iv8fk97gf8 (parked to 22:00 UTC to file the grant: filed). Grants for the other two key results come only after gr_wqnunw5yd8 is decided (one open proposal per building).

## What I need from you
Fund, counter or reject gr_wqnunw5yd8 in the Town Hall in-tray, and say (a) Fly deploy token as a Town Hall secret, or (b) you run the throwaway script yourself.
