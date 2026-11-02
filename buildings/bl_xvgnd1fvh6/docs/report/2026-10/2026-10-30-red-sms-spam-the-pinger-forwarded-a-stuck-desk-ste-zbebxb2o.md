---
id: "dc_g6zbebxb2o"
type: "report"
state: "building"
title: "Red SMS spam: the pinger forwarded a stuck desk-steal red every hour (18 SMS + 18 emails). Fixed in PR #112 (main 7820226), redeploy queued, Wright reinstalled the pinger; parked for the live check"
authorId: "ag_bcszgwmgz0"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["mt_l8rcsvyosg","dc_mkwtks9g73","dc_9w92tzhem6"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/112"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Cause confirmed (pinger hourly backstop on a stuck desk-steal red, value 0), fix merged (PR #112, main 7820226), pinger reinstalled by Wright. The live check is already parked as as_nnhl2nm5oc (waits deploy 7820226); no second assignment. Rollup #21 goes out once that check reports alerts empty and the pinger quiet."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-30T17:13:54.053Z"
sessionId: "se_ax78dwqb56"
assignmentId: "as_seigayuqpg"
costUsd: 1.3568004000000002
tokens: 67840
turns: 28
createdAt: "2026-10-30T17:13:13.577Z"
updatedAt: "2026-10-30T17:13:54.053Z"
---
## What I did
- Checked live health and asked Wright for the pinger's journal and state file. That confirmed the cause.
- Fixed the server monitor and the pinger in one PR (https://github.com/mitchellgordon95/muster-town/pull/112). CI is green; I merged it (**main 7820226**) and queued a redeploy.
- Wright reinstalled the pinger from main.
- Parked until 7820226 is live to do the live check.

## Findings
**What caused the texts**
- At 17:02Z, GET /api/health showed `monitor.outbound: false`. Its only alert was `desk-steal` red since 2026-10-29 23:28Z, with **value 0**.
  - A clean session had already come in, but the alert only clears after 5 clean ended desk sessions of at least 5 min. Not enough have ended since the move to perf-1x, so it never cleared.
- Wright's journal shows the pinger's backstop forwarded that red **once an hour**: 18 SMS + 18 emails `[muster.town] RED: desk-steal`, from Oct 29 22:31 ET to Oct 30 12:36 ET, with no send failures.
  - Every probe in between logged `ok (fails 0)`, so the health check itself never failed.
  - State file: `forwarded: {"desk-steal": …}`. The old rule was REALERT_S = 3600 per key.

**What changed (PR #112)**
- **Server monitor:** metrics can now give `expireMs`.
  - If a `desk-steal` alert is open and no desk session ends for 3 h, it now clears and is marked stale (the event carries `stale: true`, and the FYI says so).
  - Alerts saved before this change have no last-reading time, so the code uses `since` instead. The live alert should therefore clear on the first sample after deploy.
  - New test added. All 29 monitor tests and the typecheck pass.
- **Server monitor:** a red that stays red now re-alerts every 6 h instead of every hour. This matters once the ALERT_* secrets are set.
- **Pinger (deploy/pinger/muster_pinger.py):** it now forwards a server red only when something changes:
  - once when a key turns red,
  - a "still RED" reminder every 6 h while it stays red,
  - one "cleared" message when it goes away.
  - The reminder while health is down is now 6 h as well. I simulated 400 one-minute probes; it sent 1 RED + 1 reminder, then 1 cleared.
  - deploy/README.md is updated to match.
- **Wright's answer:** "Reinstalled and confirmed … Line 38 of the installed file: `REALERT_S = 6 * 3600`. Compiles clean. State file untouched … next reminder would be 22:36Z unless the red clears first, in which case you'll get the single 'cleared' message." His last journal lines are `ok (fails 0)`.
- **What happens next:** once 7820226 is live, Mitchell should get exactly one `[muster.town] cleared: desk-steal` SMS + email, and then nothing more.
- **Not checked yet:** health on 7820226, and whether the pinger has really gone quiet. That is the parked continuation. The topic page [dc_9w92tzhem6](../../wiki/2026-10/2026-10-29-monitoring-and-alerting-92tzhem6.md) has the plan.

## What I need from you
Nothing needed.
