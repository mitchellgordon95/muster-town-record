---
id: "dc_k7peu0s6wu"
type: "report"
state: "building"
title: "Docs wiki layer proposed as grant gr_7rkuduijhq (one living page per job, 350k); ships now, not after the refactor"
authorId: "ag_x3f3nn9mh8"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Taken in. gr_7rkuduijhq is proposed with its card in the Town Hall queue; Mitchell said in mt_dm14dgejml (18:08Z) the proposals are fine and he is going through the queue himself, so nothing more to file. Checked the main snapshot (9defeb5): docs/engineering-jobs-and-threads.txt:91 still lists step 8 as not planned and no log.d entry after 11-15 from Mitchell's outside session, so \"ships now\" and the stop condition on 9a stand as written."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-16T18:13:12.804Z"
sessionId: "se_8merld960x"
assignmentId: "as_km7e0024vi"
costUsd: 0.7833668000000001
tokens: 39168
turns: 14
createdAt: "2026-11-16T18:10:34.880Z"
updatedAt: "2026-11-16T18:13:12.804Z"
---
## What I did
Read meeting mt_dm14dgejml (decision 6), the job plan [dc_uwx045472m](../../../../workshop/docs/note/2026-11/2026-11-10-plan-the-job-abstraction-plan-and-cost-for-mitchel-x045472m.md), docs/engineering-jobs-and-threads.txt, packages/core/src/jobs.ts and memory.ts (topicOf pages), and checked open PRs and Mitchell's refactor branches. Filed the proposal with its card; wrote topic page [dc_plrsk6u0gq](../../wiki/2026-11/2026-11-16-job-pages-docs-wiki-layer-rsk6u0gq.md).

## Findings
- **Proposal gr_7rkuduijhq** "One living page per job", goal gl_i9gm1fodgo, ask 350,000 (M+M+S; estimate: 3 similar grants spent 328,940–368,334). KRs kr_49fzos8jaj (11-23), kr_e8cr3mxhay (11-26), kr_6n8wa45i09 (11-28).
- **Design:** submit_report takes `page`, the job page rewritten whole by the session that already holds the context (no template, no extra LM call). Stored as a wiki doc keyed to the job (topicOf building + new docs.jobId), revisions kept; a grant/directed step report without it is refused (avoid-fallbacks rule). The next session's first message carries the page instead of the raw thread. Step 2: GET /api/jobs/:id and the grant page show it first. Step 3: pages for open jobs, a manual line, Kelly folds the onboarding facts in.
- **Ships now, not after the refactor:** plan steps 1-7 (jobs, entries, answer loop, asks over threads, rollups and outbox gone) are on main; Mitchell's last branch claude/jobs-asks-rollups-outbox merged 2026-11-12. Still open: step 8 (Secretary per captain), 9a (web reads threads), 9b (stop writing report docs). Step 2 builds on 9a, or stops and folds into Mitchell's PR if he starts 9a first (in the stop condition).
- This building now has two open proposals: gr_eztubyh7nf (fallbacks) and gr_7rkuduijhq.

## What I need from you
Fund, counter or reject gr_7rkuduijhq in the Town Hall queue.
