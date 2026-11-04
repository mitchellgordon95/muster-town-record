---
id: "dc_zq0j0km04l"
type: "report"
state: "building"
title: "gr_n0p3ast5pp step 3: health `capacity` block in PR #289, parked on its CI"
authorId: "ag_ox1ugw5xd5"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: PR #289 (capacity block) is ready; its merge continuation as_nx4iupm427 is held because gr_n0p3ast5pp crossed 100 % again. The checkpoint session folds it in."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-04T00:45:22.958Z"
sessionId: "se_aez6lwxzr1"
assignmentId: "as_uunirbls61"
costUsd: 1.0982132000000002
tokens: 54911
turns: 9
createdAt: "2026-11-04T00:26:02.752Z"
updatedAt: "2026-11-04T00:45:22.958Z"
---
## What I did
I added a `capacity` block to GET /api/health. The work is in PR https://github.com/mitchellgordon95/muster-town/pull/289. It covers capacity.ts, its wiring in app.ts, context.ts, routes/town.ts and main.ts, tests in health.test.ts, and the field names in docs/scaling.md. I kept it lean, as Cleo asked.

What I checked:
- `npm run typecheck`: green.
- `test/health.test.ts`: 5/5 pass.
- The full server suite was still running on my desk when I filed this, so I'm relying on the PR's CI for it.

I rewrote the topic page "Monitor internals" ([dc_orhwzyxs59](../../wiki/2026-10/2026-10-29-monitor-internals-hwzyxs59.md)) with a "Capacity block" section. Next step: merge when CI is green, then verify the block live.

## Findings
- **Shape:** `capacity: {at, wsClients:{now, ceiling:1200}, tick:{p95Ms, slowMs:500, samples}, db:{mb, volumeGb}, restarts24h}`. It is computed in the 5 s HealthCache refresh, never on the request path, and only on the root app.
- **Tick:** a ring keeps the main runtime's last 100 distinct `tickStats().last` values, skipping repeats of the same `at`; p95 is nearest-rank. Hosted worlds' ticks are not included. `tickStats()` is reachable through `app.runtime`, so runtime code is unchanged.
- **restarts24h:** nothing was recorded once per start, so main.ts now writes a boot marker (`markBoot`: a `system` event "Server started" with `payload.boot`). No migration was needed. The probe reads the last day's markers once when it is built, so refreshes don't query SQLite. It shows 1 right after the first deploy and rises with each restart from then on.
- **db:** stat of town.db plus -wal, in MB. statfs of the db's directory gives the total in GB. With an in-memory test database it reports mb 0 and the GB of the filesystem holding the server's working directory.
- **For step 4 (ws stringify-once):** I rewrote only the "How to check headroom live" section of docs/scaling.md: the table now uses nested names (`wsClients.now`, `tick.p95Ms`, `db.mb`, `restarts24h`) and the old "Until step 3 lands" line is gone. Step 4's before/after numbers belong in the bottleneck table or its own section; don't touch this one. If both PRs are open at once, rebase on main.

## What I need from you
Nothing needed.
