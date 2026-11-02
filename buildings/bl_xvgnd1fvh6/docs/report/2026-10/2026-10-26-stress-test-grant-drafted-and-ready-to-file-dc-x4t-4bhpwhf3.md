---
id: "dc_cr4bhpwhf3"
type: "report"
state: "building"
title: "Stress-test grant drafted and ready to file (dc_x4twxh1a8o); parked until 22:00 UTC because the Prod key result doesn't exist yet"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_x4twxh1a8o","dc_qg2gppz9jd","dc_vxgg8r55ha"],"urls":["https://muster.town/api/buildings/bl_xvgnd1fvh6","https://muster.town/api/town"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. The parked continuation (files the grant from dc_x4twxh1a8o at the 22:00 UTC check) already exists, so no new assignment. The ask (Mitchell writes the Prod key result) goes into Prod rollup #3 now."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-26T15:20:18.286Z"
sessionId: "se_78vrj8rszo"
assignmentId: "as_1soi2qnkbi"
costUsd: 2.72125565
tokens: 28140
turns: 28
createdAt: "2026-10-26T15:19:52.893Z"
updatedAt: "2026-10-26T15:20:18.286Z"
---
## What I did
Checked the condition: at 15:20 and again at 15:40 UTC the Prod building has no key result (`keyResults: []`, budgetMode open), and `propose_grant` requires one of the building goal's key results, which only a human writes. So instead of filing, I wrote the complete proposal as a note in the Prod cabinet, [dc_x4twxh1a8o](../../note/2026-10/2026-10-26-stress-test-grant-the-proposal-as-filed-throwaway-twxh1a8o.md), with every `propose_grant` field ready (objective, approach, stop condition, token ask, five testing-plan lines, note for Mitchell), grounded in the live architecture rather than guesses. Parked the assignment until 22:00 UTC (the hour Pix re-checks the Workshop key result); the continuation files the grant in one call if the key result exists.

## Findings
- **Live town, measured 2026-10-26 15:20 UTC:** one Fly Machine shared-cpu-2x / 2 GB (iad), SQLite single writer, commit 119bd70; 13 agents, 4 buildings; the WS snapshot (`GET /api/town`) is 26 KB and answers in ~50 ms from a desk in the same region; session slots 3 running of max 6. Nothing was loaded or written on the server.
- **The current agent cap is stale:** `desks.maxRunning = 6` came from the OVH box's memory ([dc_vxgg8r55ha](../../note/2026-10/2026-10-21-stress-test-how-many-desks-muster-prod-1-ovh-d2-8-gg8r55ha.md), ~900 MB per compiling desk on 7.6 GB). Desks are now separate 2 GB Fly Machines, so the real ceiling for agents is the town server's per-session work, the Fly API (the runtime polls each desk every 1.5 s) and the Claude org limits (one killed a session on 2025-10-25), none of which has been measured.
- **Bottleneck candidates from the code, ranked, unmeasured:** (1) every change (`agents.pos` per tile step of each walking body, every event, building updates) is stringified separately for every WebSocket client on the one Node thread, with an 8 MB "too slow" cutoff (packages/server/src/ws.ts); (2) synchronous SQLite writes on the event loop, one per tile step per walking body plus every verb (packages/core/src/world/movement.ts); (3) the 2 GB Machine; (4) Fly API polling and Machine starts per session; (5) Claude org limits.
- **The proposal ([dc_x4twxh1a8o](../../note/2026-10/2026-10-26-stress-test-grant-the-proposal-as-filed-throwaway-twxh1a8o.md)):** two loads measured separately in announced windows, viewers (N read-only WebSocket clients, ramp 10 → 400) and agents (scripted visitors over the API, no tokens; then `maxRunning` 6 → 8 → 12 with real cheap-model sessions), each ramp stopped at the first failure signal, the bottleneck being the metric that broke first, reproduced twice. Includes a read-only load block on `/api/health`. Ask: 10 M tokens (≈ $15 at my $1.54/M blended rate; the stoplight cost 4.3 M), of which the real-session step is capped at 2 M. Stop condition and abort rule (two degradations of the live town → stop) are in the note. Option offered: ramps on a throwaway clone Machine first if Mitchell prefers not to load production.
- **What I don't know:** where any number lands (nothing measured yet), the documented Fly and Claude limits (not readable from a desk), and real users' latency (a desk in iad doesn't represent it; server-side lag is the primary number).

## What I need from you
Mitchell writes the Prod key result in Prod → Settings → Key results (the town-hall draft text: "A stress test reports the max concurrent users/agents the live town supports and names the first two bottlenecks"); the grant files itself at the next check after that.
