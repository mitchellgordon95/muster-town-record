---
id: "dc_3lkisf9v80"
type: "report"
state: "building"
title: "Jobs and entries, read only: PR #432 open, parked on CI"
authorId: "ag_7q3sjb4l00"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 1 of gr_9mp6v6vv8k built: PR #432 (migrations 110 jobs, 111 entries; GET /api/jobs/:id; core + server tests) open on CI. Its continuation as_lk81c9cgjx already waits on {pr: 432} and merges on green, then live-checks the endpoint. Nothing more to queue; step 2 queues from the finished step report."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-12T15:28:52.054Z"
sessionId: "se_6hhwqwkc03"
assignmentId: "as_6bfvwm7yly"
costUsd: 3.5708866000000006
tokens: 178544
turns: 71
createdAt: "2026-11-12T15:28:37.319Z"
updatedAt: "2026-11-12T15:28:52.054Z"
---
## What I did
Built step 1 of gr_9mp6v6vv8k (step 3 of plan [dc_uwx045472m](../../note/2026-11/2026-11-10-plan-the-job-abstraction-plan-and-cost-for-mitchel-x045472m.md)) on branch agent/pix-2/jobs-and-entries-read-only-tables-back-f and opened draft PR #432: https://github.com/mitchellgordon95/muster-town/pull/432. This session is parked on its CI. When it resumes it merges on green, then checks the endpoint on the live server.

## Findings
- **Migration numbers:** 110 `jobs` and 111 `entries`. Main already had 109 (join_funnel_doors), and no open PR uses 110 or 111. Beyond the assignment's columns I added two: `jobs.closedAs` (the plan's A1 calls for it) and `entries.docId` (the source report).
- **Jobs (`packages/core/src/jobs.ts`).** Ids are deterministic:
  - `jb_<gr_…>`: rule ceiling. The grant's checkpoint maps to held; cut, stopped and done map to closedAs.
  - `jb_<sc_…>`: per-run, for retainer schedules.
  - `jb_<chainId>`: chunk, for exploration. Its pocketRef is the Bank reservation. It closes as done or nothing-found.
  - `jb_<building>_<source>`: pocket, for directed work with a human source.
  - `jb_<building>`: building, for everything else, including rollups and town-written in-tray rows.
- **Entries:**
  - One per report doc. It carries the verdict as `proposes`, the grant step as `moved.stepsDone`, and the Bank's booked adjusted tokens.
  - The manager's or a human's decision on a report is an entry that answers it.
  - Every grant history action (propose, fund, counter, cut…) and every retainer decision is an entry.
  - Draft grants and draft docs are left out.
- **When it syncs:** at boot (idempotent: existing entries keep their seq, new ones are appended), and again for the one job a read asks for.
- **Endpoint:** `GET /api/jobs/:id` accepts a jb_ id or a grant, schedule, building or assignment id. It returns `{job, entries, total}` and pages with `?from=&limit=` (at most 200).
- **Speed, on 6,000 synthetic reports:** the first back-fill took 0.8 s, later boots 0.4 s, and one read 60–110 ms.
- **Tests:** `core/test/jobs.test.ts` covers a funded grant (rule ceiling, propose and fund first, then one entry per step report in order, and a decision answering its report), building, pocket and chunk jobs, idempotency, and held/cut grants. `server/test/jobs.test.ts` covers the route, 404 and 400.
- **Check results:** `npm run check` passed docs, deadcode, typecheck, and the tests in core, runtime, server, cli and desk. The web workspace failed: 4 files can't load `happy-dom` because it isn't installed on this desk. I didn't touch web code, and CI will run it.
- **Gap until step 2:** nothing writes the tables live, so between boots a job only refreshes when it is read. Step 2 should reuse `JOB_OF_ASSIGNMENT` so live entries land on the same job ids. The topic page is [dc_skk467jd88](../../wiki/2026-11/2026-11-12-jobs-and-entries-gr-9mp6v6vv8k-k467jd88.md).

## What I need from you
Nothing needed.
