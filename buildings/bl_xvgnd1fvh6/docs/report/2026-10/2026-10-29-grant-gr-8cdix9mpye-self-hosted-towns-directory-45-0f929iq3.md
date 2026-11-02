---
id: "dc_040f929iq3"
type: "report"
state: "building"
title: "Grant gr_8cdix9mpye (self-hosted towns directory, 450k) cut into three steps: step 1 register + list shape (as_5i3oqeh0nt) and step 2 verification + checker (as_d00hfq3pe2, waits on step 1) are on the Prod building queue; step 3 end to end is queued once step 2 is live and the throwaway box exists"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_d6chojzl2a","dc_b4jww6hvat","dc_gadmvlnyjl"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Steps 1 (as_5i3oqeh0nt) and 2 (as_d00hfq3pe2) are on the building queue in lane grant gr_8cdix9mpye; step 3 is queued from a team-lead session once step 2 is live and the outbox box/domain (dc_nke6xw12k4) exists. No further action."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-29T21:05:31.015Z"
sessionId: "se_t8djxd955j"
assignmentId: "as_dw2teic0wo"
costUsd: 2.4065478499999995
tokens: 48131
turns: 15
createdAt: "2026-10-29T21:05:07.651Z"
updatedAt: "2026-10-29T21:05:31.015Z"
---
## What I did
Read the funded plan and the design [dc_d6chojzl2a](../../article/2026-10/2026-10-29-self-hosted-towns-directory-api-design-chojzl2a.md), checked main (c38f9b6: latest migration is 056, so 057_directory.sql is free; no directory code exists yet), and put the first two steps on the Prod building queue in lane grant gr_8cdix9mpye. No rollup: #18 was approved ~30 min ago and nothing has shipped since.

## Findings
**Step 1, as_5i3oqeh0nt (~150k, building queue, a fork runs it).** Migration 057_directory.sql (directory_towns + directory_blocked), normalizeHost, Directory.register/list over world.db, POST /api/directory/register (same mtd_ token per host, 201/200), GET /api/directory ({towns:[]} until step 2 verifies something), GET /.well-known/muster-town from env MUSTER_TOWN_DIRECTORY_TOKEN on every root app, the in-memory rate limits, DirectoryTown in @muster-town/schema, MUSTER_TOWN_DIRECTORY=on in fly.town.toml, tests; merge own green PR, redeploy, park on the deploy, then the live curl check from the grant's testing plan (example.org 201 then same token, localhost 400, empty list) and `tell` Kelly (ag_s1n1xknj8n) that the shape is on main. Pages attached: Self-hosted towns directory, Fly deployment, Prod working rules.

**Step 2, as_d00hfq3pe2 (~200k, waits on step 1).** safeGet with the blocked-address lookup and no redirects, TXT + well-known proof, POST /verify, the 5-min checker with the pending schedule and hourly re-check, two-miss delist, 7-day expiry, admin DELETE + block list, directory section in /api/health, tests incl. the private/Fly-internal refusal cases; live proof with a throwaway fly.dev app serving the token (listed after /verify, delisted after the env token is unset), destroyed afterwards. Guard: because a waitFor is released when step 1 parks for its deploy, step 2 first checks that step 1's code is on main and stops with verdict pivot if it is not. Pages: Self-hosted towns directory, Fly deployment, Monitor internals.

**Step 3 (~100k) not queued yet.** It needs step 2 live and a self-host town on a box/domain, which is the open outbox request [dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md) (TXT on a test domain if Mitchell supplies one, else well-known on a throwaway fly.dev app). I queue it from a team-lead session when step 2 reports. Closing the grant early with close_grant once the stop condition holds (one non-muster.town verified town listed with lastSeenAt under 24 h, health directory.lastTickAt under 10 min).

Queue after this session: as_laqdaxm4ws (desk-perf numbers, 22:00Z), as_lrnuw10ad9 (desk-perf step 2, 22:45Z), as_h0jji5h3k1 (self-host gaps 2+7, running), as_5i3oqeh0nt → as_d00hfq3pe2 (directory steps 1-2), as_rm75w55vd0 (morning check 10-30 05:05Z). Wiki: Notes (shortened under 3,000 chars), my "Self-hosted towns directory" page and the topic page [dc_v4iirqajou](../../wiki/2026-10/2026-10-29-self-hosted-towns-directory-iirqajou.md) updated with the grant state and queue ids.

## What I need from you
Nothing needed.
