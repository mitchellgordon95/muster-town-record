---
id: "dc_8ej0m0ycmq"
type: "report"
state: "building"
title: "Desk perf step 2 live: a real desk-steal red (85%) fired at 23:28:58Z, event 57050, FYI dc_qrhf8jup1j; no SMS or email because outbound is off"
authorId: "ag_9xsvk2pq8s"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 2 of gr_uhh6u39vv9 verified live by a real red (85% steal, event 57050). The FYI wording nit goes on the queue as its own small fix. Step 3 waits for Mitchell's call in rollup #19."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-29T23:30:08.825Z"
sessionId: "se_an9vestabd"
assignmentId: "as_vt8eovf938"
costUsd: 0.7128952000000001
tokens: 35645
turns: 17
createdAt: "2026-10-29T23:29:52.736Z"
updatedAt: "2026-10-29T23:30:08.825Z"
---
## What I did
- **Confirmed the code is live.** Health shows commit 473f871 (server started 23:26:58Z), and c229d63 is an ancestor of it.
- **Did not run the forced test.** `POST /api/admin/monitor/test?metric=desk-steal` needs an admin *user* token. The only tokens on this desk are agent tokens, and both get a 403. The desk also has no flyctl.
- **Recorded a real alert instead.** A natural red `desk-steal` alert fired on the first sample after the deploy, and I recorded it. That shows more than the forced test would have, because it went through the real path.
- Rewrote the topic page "Monitoring and alerting" ([dc_9w92tzhem6](../../wiki/2026-10/2026-10-29-monitoring-and-alerting-92tzhem6.md)).

## Findings
- **The real red alert, raised 2026-10-29 23:28:58Z:**
  - **Session:** se_fxm970b4no ended 23:28:34Z. Wall time was 555.7 s, cpu 80.8 s and steal 467.1 s, so the steal share was **85 %**.
  - **Town event:** id **57050**, "Alert raised RED: desk session steal 85% of cpu + steal (desk-steal)".
  - **Prod FYI:** **[dc_qrhf8jup1j](../../fyi/2026-10/2026-10-29-cleared-red-desk-steal-desk-session-steal-5-of-cpu-hf8jup1j.md)**, "[RED] desk session steal 85% of cpu + steal".
  - **Health:** `monitor.alerts` = [{key: desk-steal, level: red, value: 85}], and lastSampleAt is fresh.
- **No SMS or email went out.** `monitor.outbound` is still false because the ALERT_* secrets are unset; the request is already in outbox dc_nwv9dy37ui, so I'm not asking again.
- **This matches the measured 84–91 % steal.** Under the kept 50/35/25 thresholds, desk-steal will stay red while desks run on shared CPUs. That is the evidence step 3 needs.
- **Small wording bug in the FYI.** It says the alert clears "after 5 samples in a row under yellow", but desk-steal clears after 5 clean *sessions*. Only the FYI text is wrong, not the behaviour. I didn't fix it here.
- **Step 2 of gr_uhh6u39vv9 is done.** Step 3 stays unqueued until Mitchell gives his word on rollup #19.

## What I need from you
Nothing needed.
