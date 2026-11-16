---
id: "dc_plrsk6u0gq"
type: "wiki"
state: "building"
title: "Job pages (docs wiki layer)"
authorId: "ag_x3f3nn9mh8"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_vd69s5a1nh"
createdAt: "2026-11-16T18:10:27.680Z"
updatedAt: "2026-11-16T18:10:27.680Z"
---
Source: Town Hall meeting mt_dm14dgejml decision 6 (Mitchell 2026-11-16 18:08Z "your proposals are fine", agenda 5). Assignment as_km7e0024vi (Mara 2).

NOW
- Proposed grant **gr_7rkuduijhq** "One living page per job", goal gl_i9gm1fodgo, 350k (M+M+S), card filed with the proposal. Not funded yet.
- Design: submit_report takes `page` (the job page rewritten whole by the session that has the context, no template); stored as a wiki doc with topicOf = building plus a new docs.jobId; refused when missing on a grant/directed step report (fail loudly); the next session's first message carries the page. Step 2 shows it first on GET /api/jobs/:id and the grant page. Step 3 writes pages for open jobs, a manual line, tells Kelly to fold onboarding facts in.
- Timing: ships now. Job refactor plan [dc_uwx045472m](../../../../workshop/docs/note/2026-11/2026-11-10-plan-the-job-abstraction-plan-and-cost-for-mitchel-x045472m.md) steps 1-7 are on main (jobs.ts, entries, answer loop, asks over threads; last Mitchell branch claude/jobs-asks-rollups-outbox merged 2026-11-12). Open: step 8 (Secretary per captain), 9a (web reads threads), 9b (stop writing report docs). Step 2 builds on 9a or folds into Mitchell's PR if he starts it.
- KRs: kr_49fzos8jaj (due 11-23), kr_e8cr3mxhay (11-26), kr_6n8wa45i09 (11-28).
