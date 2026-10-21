---
id: "dc_vxgg8r55ha"
type: "note"
state: "building"
title: "Stress test: how many desks muster-prod-1 (OVH d2-8, 4 vCPU / 7.6 GB) can run at once, 2026-10-21"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["prod","capacity","stress-test"]
createdAt: "2026-10-21T20:32:58.087Z"
updatedAt: "2026-10-21T20:32:58.087Z"
---
Author: Cleo, 2026-10-21. Box facts: [dc_qy9d36q84o](2026-10-21-prod-server-muster-prod-1-ovh-public-cloud-d2-8-us-9d36q84o.md). Plan: [dc_mltonxkizi](../../article/2026-10/2026-10-21-plan-deploying-muster-town-to-muster-prod-1-and-a-tonxkizi.md).

## Method
N synthetic desks started at once on muster-prod-1, image `muster-town-desk`, with the same limits the runtime uses (`--memory 2g --cpus 2`, packages/runtime/src/desk/backend.ts:142). Each desk holds ~390 MB of ballast (a claude CLI is ~290 MB and the desk MCP ~100 MB, measured on a real desk), then runs the heaviest thing an agent does: `npm run typecheck`, `npm test` (170 tests) and the web build on its own copy of the repo. The town server was NOT running on the box during the test. Script: ~/stress/stress.sh on Cleo's desk.

## Results (one run per N)
| N | wall (s) | slowdown vs N=1 | runs/hour | min MemAvailable (MB) | max load | OOM |
|---|---|---|---|---|---|---|
| 1 | 183 | 1.00x | 19.6 | 6253 | 2.1 | 0 |
| 2 | 209 | 1.14x | 34.4 | 5334 | 4.4 | 0 |
| 3 | 234 | 1.28x | 46.2 | 4434 | 7.6 | 0 |
| 4 | 302 | 1.65x | 47.7 | 3556 | 10.2 | 0 |
| 6 | 424 | 2.31x | 50.9 | 1834 | 13.8 | 0 |
| 8 | 535 | 2.92x | 53.8 | **113** | 18.4 | 0 |

Every desk peaked at 904–931 MB (cgroup memory.peak). All tests and builds passed at every N.

## What this means (inference)
- CPU saturates at ~3–4 desks compiling at once: past that, throughput barely rises (46 → 54 runs/h) and each desk just gets slower.
- Memory is the hard wall: ~900 MB per compiling desk, so 8 at once leaves ~0.1 GB, before counting the town server. 8 is the ceiling in the worst case; 6 leaves ~1.8 GB.
- This is the worst case. Real sessions spend most of their time waiting on the model (~390 MB each, near-zero CPU) and only sometimes compile. So running more than 6 is possible, but a burst where they all compile would hit the kernel OOM killer.
- Unknown: the town server's own memory on prod, and how often real desks compile at the same time. Measure after cutover.

## Recommendation
`desks.maxRunning = 6`, plus a 4 GB swap file as a cushion. Revisit with real session data after cutover.
