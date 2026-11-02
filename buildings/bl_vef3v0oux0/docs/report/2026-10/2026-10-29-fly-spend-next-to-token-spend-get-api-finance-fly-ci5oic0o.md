---
id: "dc_h2ci5oic0o"
type: "report"
state: "building"
title: "Fly spend next to token spend: GET /api/finance/fly and a \"Hosting (Fly.io)\" section on the finance page, on main at b380807 (Mitchell's ask via Cleo); live check and picture queued for the fork"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["mt_s6f8mvjw9h","dc_wgen2enl3j","dc_ph7t36geb8","dc_ns3ft53d9u","dc_tkzoy81p4b","dc_nb3743g7f6"],"urls":["https://docs.fly.io/about/pricing","https://github.com/mitchellgordon95/muster-town/commit/b380807"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "b380807 on main (GET /api/finance/fly + Hosting (Fly.io) section, tests green, Mitchell's directed ask via Cleo). Live check, picture and topic-page rewrites already running as as_6ailpm6r90 (waitFor deploy b380807). Rollup when that reports."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-29T23:56:31.995Z"
sessionId: "se_prz6tau0t0"
assignmentId: "as_z99cbqvxtj"
costUsd: 8.147644349999998
tokens: 162953
turns: 79
createdAt: "2026-10-29T23:56:11.670Z"
updatedAt: "2026-10-29T23:56:31.995Z"
---
## What I did
Took Cleo's brief for Mitchell (1:1 mt_s6f8mvjw9h): Fly spend in the Bank's accounting, next to token spend. Read the sessions schema (wallMs/cpuMs/stealMs since b851a0e, desk sessions have backend "docker" even on Fly), the Fly desk backend (packages/runtime/src/desk/fly.ts: shared 2 vCPU 2048 MB defaults), fly.town.toml ([[vm]] shared-cpu-2x 2 GB), Prod's desk-perf reports ([dc_ph7t36geb8](../../../../bl_xvgnd1fvh6/docs/report/2026-10/2026-10-29-desk-session-performance-key-result-kr-4pf0n8q9jl-7t36geb8.md), [dc_ns3ft53d9u](../../../../bl_xvgnd1fvh6/docs/report/2026-10/2026-10-29-prod-rollup-19-desk-sessions-show-cpu-and-steal-84-3ft53d9u.md)) and Fly's price list (docs.fly.io/about/pricing). Built the endpoint and the page section myself (it is Bank code; Mitchell's directed ask), tests green, pushed straight to main under the building's merge rule after a rebase (main had moved to c01dd81 under me; a first push failed, no harm). Told Cleo twice (ms_xx5vwcp0zr with the shape and two asks for Prod's step 3; ms_c3xws7j6un with the corrected sha). Queued one directed fork assignment (as_6ailpm6r90, waitFor deploy b380807): verify live, run `npm run check:finance`, one cropped picture, rewrite the pictures and endpoints topic pages. Rewrote topic pages [dc_tkzoy81p4b](../../wiki/2026-10/2026-10-29-the-three-finance-endpoints-their-sum-checks-and-l-zoy81p4b.md) and [dc_nb3743g7f6](../../wiki/2026-10/2026-10-29-the-bank-page-bankpanel-bankfinance-its-tests-and-3743g7f6.md) and my wiki.

## Findings
- **Commit b380807 on main** (CI promotes to prod; live was c01dd81 at 00:05Z). Files: packages/core/src/finance-fly.ts (new), bank.ts (`Bank.fly`), server routes/town.ts (`GET /api/finance/fly?days=`), web api.ts + mock/server.ts + panels/FinancePanel.tsx (`FlyView`), scripts/finance-check.ts (15 → 18 checks), docs/architecture.md, docs/log.md. Tests: core finance-fly 10 (one pins `TOWN_MACHINE` to fly.town.toml), web finance 23 (5 new), REST 21; `npm run typecheck` 17 s, check:docs green.
- **What the endpoint says, in US dollars, never from Fly's bill.** Per UTC day over a window (default 30 d, `?days=` 1..90): desk sessions (backend ≠ host) × wall time (`wallMs`, else endedAt − startedAt; a running session up to now; split across midnight) × the desk Machine size's list $/h (desks config cpuKind/cpus/memoryMb, default shared-cpu-2x 2 GB = $13.39 / 30 d = $0.018597/h; priced only when desks.backend is `fly`), each session charged to its assignment's building else its agent's (as /spend does); plus the town Machine (shared-cpu-2x 2 GB, same rate) × hours of the day elapsed, only when the server runs on a Fly Machine (`FLY_APP_NAME`). Body: `today` (desk, town, total, cap, underCap), `days[]` with per-building rows, `buildings[]`, `totals`, `rates` (with source and pricedAt), `assumptions[]`, `notCounted[]` (volumes $0.15/GB-month, stopped rootfs, bandwidth), `sumCheck` (per day desk + town = total; Σ days deskMs = Σ buildings deskMs).
- **The page**: last section "Hosting (Fly.io)": Today / Last 7 days / Last 30 days × Desks / Town Machine / Total, a "Daily desk cap" row (none set), both Machine sizes with $/h and $/30 d, desk time and sessions (unmeasured count noted), per-building rows, "Not counted", a "How this is estimated" details, a ✓ line; footer says "(Hosting in US dollars)".
- **Preview from public data** (sessions of the 16 listed agents; forks' sessions are not listed, so a lower bound; the live endpoint reads the whole table): town Machine $0.446/day; desks 2.5–5 h/day ≈ $0.05–0.09/day at shared-cpu-2x (×2.5 at performance-1x, $0.0458/h); 7-day total ≈ $3.45. Median desk session ≈ 3.5 min (198 of 206 by endedAt − startedAt; only 3 carried wallMs in that sample). A $10/day cap is far above today's use.
- **Prices (iad, read 2026-10-29, `FLY_PRICES`)**: shared-cpu-1x 256 MB $2.19; shared-cpu-2x 2 GB $13.39; performance-1x 2 GB $33; performance-2x 4 GB $66; +$6/GB-month RAM. Cleo's "shared-cpu-1x ~$0.003/h" is the 256 MB preset; our desks are 2x 2 GB.
- **Two asks sent to Prod for desk-perf step 3** (gr_uhh6u39vv9): the cap readable by the server (then one line in the /api/finance/fly route changes from `capUsdPerDay: null`), and a per-session Machine size so sessions before a move aren't re-priced (until then `assumptions` says every session is priced at today's size).
- Not a key result yet. If Mitchell wants it tracked, a KR from the 1:1 notes, then a grant; not set unasked.

## What I need from you
Nothing needed.
