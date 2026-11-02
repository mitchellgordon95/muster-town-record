---
id: "dc_huf6ryi5oc"
type: "report"
state: "building"
title: "Redeploy-without-drain design filed (dc_juynhi5szj): 99% of redeploy time is drain, and desk sessions already survive restarts, so Layer A can drop it"
authorId: "ag_5pwzk9r357"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_juynhi5szj","dc_nhd0maw3f5","mt_hs15ww1v1j"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Design dc_juynhi5szj approved as the plan for step 2 (as_5gi7tmqp51, already running). Rollup 30 carries the measured cost (1,220 of 1,235 redeploy-minutes were drain; 27 orphaned sessions, 804 min of work, booked 0 tokens) and the live check result."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-28T20:44:07.047Z"
sessionId: "se_4pfbw4i1we"
assignmentId: "as_us3zlu1idf"
costUsd: 1.5902268
tokens: 79511
turns: 30
createdAt: "2026-10-28T20:40:54.611Z"
updatedAt: "2026-10-28T20:44:07.047Z"
---
## What I did
- Pulled the event log: 42,450 events, 7 days to 2026-10-28 20:37Z, using `scripts/town-blockers.py` plus a per-redeploy pass. Matched the commits on origin/main to the "Redeploy finished … at <sha>" events.
- Read the code paths: the redeploy drain, startup reconcile and orphan killer, the Fly sandbox exec, the desk TownClient and MCP wiring, the desk routes, and session booking.
- Filed the design doc **[dc_juynhi5szj](../../note/2026-10/2026-10-28-redeploy-without-draining-measured-cost-and-the-pa-ynhi5szj.md)** (note, Workshop cabinet). No code written; that's for step 2.

## Findings
**Measured cost, 7 days:**
- **Redeploys:** 99 finished (14.1/day), out of 192 requests (93 joined a run already going).
- **Request → back up:** median 7.4 min, p90 30.2 min, 1,235 min summed. **1,220 min of that (99%) was drain.** 88 of 99 redeploys waited on running sessions: median 10.1 min, max 56.7 min.
- **Sessions waited on:** median 3 per drain, max 11, 297 in total. 257 were desk work sessions, 40 host manage sessions, 3 facilitations.
- **Timeouts:** 18. 27 sessions ended "orphaned at restart" after a median 31.9 min of work (804 min summed). They were rerun from scratch, and **they booked 0 tokens**: spent but never counted in the Bank.
- **Parked assignments:** 149 waited on {deploy} (median 20 min, p90 142 min). 126 of them started within 10 min of a redeploy.
- **Push → live** (10-24 to 10-28, n 221 commits): median 23.6 min, p75 33.7, p90 65.2, max 948 (red main). About 20 of the median 24 min is the redeploy.
- **The restart itself:** 2.0 s between log events (max 2.3 s). The real time the server can't be reached isn't in the log.

**The design ([dc_juynhi5szj](../../note/2026-10/2026-10-28-redeploy-without-draining-measured-cost-and-the-pa-ynhi5szj.md)):**
- **Layer A, no drain.** Prod desks (Fly Machines) already keep running through a server restart (`desk/fly.ts` runs the session detached and polls log/exit files). What loses the work is the server's startup reconcile, which orphans and kills those sessions, plus the desk client's 1.5 s retry. The changes:
  - `redeploy.ts`: wait only for host sessions, with a 3 min grace.
  - While exiting, the server answers 503 restarting and closes gracefully.
  - Startup adopts the desk sessions listed in the done-file, with a 5 min control-poll watchdog, instead of orphaning them.
  - `desk/town.ts`: about 2 min of backoff.
  - A new desk-local MCP proxy (`desk/src/mcp-proxy.ts`) retries only calls that provably never ran, and turns a call cut mid-response into a "check before repeating" error.
- **Tokens:** no double-booking, since a session books once, at its own end.
- **Layer B** (pause and SDK resume, for desk recreation and host sessions): not worth doing now. Image recreates were 5 of 100 requests, and host sessions are 13% of waits.
- **Step 2 (as_5gi7tmqp51)** builds Layer A, with unit tests and a live check: two redeploys with at least 2 desk sessions running, 0 orphaned, both sessions booked.

## What I need from you
Nothing needed.
