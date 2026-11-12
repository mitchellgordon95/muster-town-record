---
id: "dc_x3fbzp82dz"
type: "report"
state: "building"
title: "/api/uptime live from UptimeRobot, 100 % matches status page; PR #441 fixes the missing status link"
authorId: "ag_17uowt6q0w"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. /api/uptime live from UptimeRobot (100 %, matches getMonitors and the status page); statusUrl bug found (UPTIME_STATUS_URL vs UPTIMEROBOT_STATUS_URL), PR #441 reads either. The parked continuation (as_44rbm57qnw) merges #441 on green CI and files the non-parked report with KR evidence; step 3 (as_70vxb55s8m) then checks the live block after the deploy."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-12T18:50:51.889Z"
sessionId: "se_mkpwrmpm1c"
assignmentId: "as_yfbsihyp3x"
costUsd: 0.8160619000000001
tokens: 40803
turns: 25
createdAt: "2026-11-12T18:50:06.726Z"
updatedAt: "2026-11-12T18:50:51.889Z"
---
## What I did
- Checked that 6185b997 is live (health at 18:45Z). Read `GET /api/uptime` and compared it with UptimeRobot's getMonitors and the public status page, both from the desk with the secrets. No secret value was printed.
- Screenshotted the landing #uptime block.
- Found that `statusUrl` was null and why. Opened PR #441 (https://github.com/mitchellgordon95/muster-town/pull/441) with the fix, a test, a deploy/README line and a log.d entry. `npm run check --fast` passes. Parked on its CI.

## Findings
- **Live /api/uptime:** source "uptimerobot", error null, 30-day pct **100**, coverage 1.7 % (the monitor started today at 06:46Z), 0 outages, 115 restart gaps. **The number matches:** getMonitors 30-day 100.000, status page ratio 100.000.
- **What a human sees now** (landing, and the same block at Bank › Hosting › Uptime): "100% up over the last 30 days · Measured by UptimeRobot; it watched 1.7% of the window". The strip has 29 grey (unknown) days and today green.
- **Bug: no link to the status page.** Mitchell saved the secret as `UPTIME_STATUS_URL`, and the code read `UPTIMEROBOT_STATUS_URL`. The secret.granted events show the name. #441 reads either name. Once #441 is live, "Measured by UptimeRobot" links the status page. That link is the last part of kr_xu6x845ycp.
- kr_z7fw2zsmu6 holds live: `POST /api/uptime/probes` returns 404. Its evidence will be filed with the non-parked report.

## What I need from you
Nothing needed.
