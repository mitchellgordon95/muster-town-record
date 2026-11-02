---
id: "dc_qwui6aewej"
type: "report"
state: "building"
title: "1ef98cc live; busy-notice code path checked (runtime 174/174), but no 1:1 with a busy agent yet, so no picture"
authorId: "ag_csjo6ks68a"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_vea3k8926p","dc_8qwqtmh7i5","mt_cvxnqawx7h"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/136"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "1ef98cc live, code path tested 174/174; no staged 1:1 possible, so rollup 34's \"Your call\" for the busy-notice item asks Mitchell to open a 1:1 with a busy agent. No picture; fine."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T01:31:55.150Z"
sessionId: "se_v2wku2vlmt"
assignmentId: "as_iaubougroq"
costUsd: 0.6743582
tokens: 33718
turns: 12
createdAt: "2026-10-31T01:31:37.596Z"
updatedAt: "2026-10-31T01:31:55.150Z"
---
## What I did
- Checked that PR #136 (1ef98cc) is live. Searched the event log for a 1:1 with an agent whose desk was busy, read the fix diff, and re-ran the runtime tests on 1ef98cc. No code changes.
- Rewrote the topic page [dc_8qwqtmh7i5](../../wiki/2026-10/2026-10-28-meetings-writing-indicator-who-ended-it-restart-dr-wqtmh7i5.md) to cover the busy notice.

## Findings
- **Live commit:** GET /api/health returns commit `1ef98cc0ace3…`, started 01:29:12Z.
- **No real case yet.** I checked the event log from 01:29:10Z to 01:31:09Z (ev 66244–66405). The only 1:1 in that window was mt_cvxnqawx7h, Mitchell with Nell. Nell was not in a work session: she answered within seconds, and Mitchell ended it at 01:30:38Z. Its only system lines are the two restart notices ("Nell's reply is waiting on a redeploy", 01:26:12Z and 01:29:10Z). Those are correct, because a restart did land mid-1:1. So no 1:1 shows the busy line yet, and I have **no picture**. An agent can't open a 1:1, so I couldn't stage one.
- **The code path is live and tested:**
  - On main, `runtime/src/manage.ts:125` (`noticeBusy`) builds the line `<Agent> is in a work session ("<assignment title, cut at 80 chars>") and answers here when it ends.`
  - `closeQuietOneOnOnes` skips a 1:1 when the human spoke last and the agent is in a non-manage session (`awaitingBusyAgent`). It now runs after `wakeManager`, and it counts quiet time from the start of the answering session.
  - Runtime tests pass 174/174 (24 files) on 1ef98cc. That includes the new test in one-on-one.test.ts: one notice, the 1:1 still open after 21 min, an answer after the work ends.
- **What Mitchell would see in a 1:1 with a busy agent:**
  1. His own line.
  2. Within about one 5 s tick, one Town line, e.g. `Nell is in a work session ("…") and answers here when it ends.` It is posted once per work session, not once per message he sends.
  3. The agent's answer, a few seconds after its work session ends.
  
  The 1:1 is no longer closed as "quiet for 20 minutes" while it waits. The agent still can't answer *during* its work session; that is as_0xss7tux3l.
- **For rollup 34:** there's no crop for this item. The "Your call" line can be: open a 1:1 with a resident whose desk is working and look for the Town line.

## What I need from you
Nothing needed.
