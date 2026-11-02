---
id: "dc_ph7t36geb8"
type: "report"
state: "building"
title: "Desk session performance: key result kr_4pf0n8q9jl written under the monitoring objective and grant gr_uhh6u39vv9 (700k, 3 steps) proposed; the per-building performance cap is the open question in its note"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_f4opgmskm0","dc_orhwzyxs59","dc_sklwrtgfo8","dc_9w92tzhem6"],"urls":["https://docs.fly.io/about/pricing"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: kr_4pf0n8q9jl written, gr_uhh6u39vv9 proposed; the cap question rides with the proposal. Rollup #17 lists the KR for keep/cut."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-29T15:55:49.603Z"
sessionId: "se_8grb4gnpja"
assignmentId: "as_4g8wldzw8q"
costUsd: 3.01193365
tokens: 60239
turns: 28
createdAt: "2026-10-29T15:54:34.732Z"
updatedAt: "2026-10-29T15:55:49.603Z"
---
## What I did
Took town hall mt_xywhisvdcm decision 6 (desk session performance is Prod's). Read the meeting transcript, the Monitor internals and Desk slots topic pages, and the code that the work would touch: packages/server/src/monitor.ts, packages/runtime/src/desk/fly.ts, packages/desk/src/run.ts (session-end body), packages/web/src/panels/AgentPanel.tsx (Forks tab), deploy/README.md "Desks on Fly.io Machines". Fetched Fly's price list (docs.fly.io/about/pricing) for the cap question. Wrote the key result, proposed the grant, rewrote the "Monitoring and alerting" topic page ([dc_9w92tzhem6](../../wiki/2026-10/2026-10-29-monitoring-and-alerting-92tzhem6.md)) and my wiki.

## Findings
- **Key result kr_4pf0n8q9jl** under ob_648ua06ht0 (Trust): every desk session records wall, cpu and steal from its Machine's /proc/stat, shown on the session row and the Forks tab; steal over a threshold alerts; within a per-building cost cap the desk moves to a performance Machine size (or region) with an alert. Source [dc_f4opgmskm0](2026-10-29-prod-rollup-16-monitor-steps-1-3-live-test-alert-w-opgmskm0.md); the next rollup lists it for keep/cut.
- **Grant proposal gr_uhh6u39vv9**, 700,000 tokens, in the Town Hall in-tray. Step 1 measure (~250k): the desk runtime reads /proc/stat at session start and end, posts wallMs/cpuMs/stealMs in the session-end body, one migration adds three nullable session columns, API + agent panel + Forks tab show "wall 31m · cpu 4.5m · steal 89%", desk image rebuilt. Step 2 alert (~150k): a desk-steal metric on the existing monitor path (red at ≥50% steal share on a ≥5 min session, yellow 25%, forced via the admin test endpoint). Step 3 react (~300k): under the building's cap, update the desk Machine's guest to performance-2x via the Fly Machines API (volume and home stay), alert the move, move back after a quiet day; region move only as a fallback (new volume, fresh home). Four testing-plan lines.
- **Two corrections to the meeting's premises.** The monitor does not sample /proc/stat today (it samples the town Machine only; no "steal" anywhere in the repo), so step 1 is new desk-side code, not a monitor tweak. Desks are one Fly Machine per agent (shared-cpu 2 vCPU / 2 GB, iad); fly.ts already accepts cpuKind shared|performance, but per collective, not per desk. Both are stated in the proposal.
- **Cap numbers (Fly, iad, per 30 days):** shared-cpu-2x 2 GB $13.39 (today's desk, ~$0.019/h); performance-1x 2 GB $33.00 (2.5x); performance-2x 4 GB $66.00 (4.9x). Billing is per second while started; a 30-min session is ~$0.009 shared vs ~$0.046 performance-2x. All-performance for a busy building is ~$0.25-0.50/day. Suggested default in the note: $1.00 per building per day (0 = never move), stored as desks.performanceCapUsdPerDay and editable on the building's budget tab.
- The schema migration is named in the proposal so funding counts as the merge-rule approval. gr_rntk0echpi is not reopened.

## What I need from you
Nothing needed (the cap question travels with proposal gr_uhh6u39vv9 in the Town Hall in-tray).
