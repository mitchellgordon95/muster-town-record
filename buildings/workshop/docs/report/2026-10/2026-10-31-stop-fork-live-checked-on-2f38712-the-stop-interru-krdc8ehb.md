---
id: "dc_d7krdc8ehb"
type: "report"
state: "building"
title: "stop_fork live-checked on 2f38712: the stop interrupt kills the fork in 4.5 s (same desk-death bug as tells); graceful wrap-up and the 5-min hard stop untested until the fix lands"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_ikie1ugt73","dc_4x9k9lmfie","dc_f11njk7cho","dc_2337yf719x"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. Controlled reproduction for diagnosis as_gtfnmftisk (interrupt with now: true during Bash kills the session in 4.5 s). The stop_fork graceful-path re-run is queued to me, waiting on the tell live check as_lx3zdkroo3 (which itself waits on the fix)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T02:14:28.342Z"
sessionId: "se_0bj60qz734"
assignmentId: "as_wv0a2u6u2x"
costUsd: 2.8907348499999994
tokens: 57815
turns: 31
createdAt: "2026-10-31T02:14:00.038Z"
updatedAt: "2026-10-31T02:14:28.342Z"
---
## What I did
What Mitchell can do now: the manager can call stop_fork on a live fork and the town records the request with a 5-minute hard-stop deadline. What he cannot rely on yet: the fork wrapping up and filing its own report, because the stop's interrupt kills the desk session within seconds, exactly like a `tell` does tonight.

Steps run as the manager (forks lack building.assign, [dc_4x9k9lmfie](2026-10-31-stop-fork-is-live-91c33c7-but-a-fork-can-t-run-its-9k9lmfie.md)):
1. GET /api/health: commit 2f38712 (started 02:06:37Z); `git merge-base --is-ancestor 91c33c7 2f38712` succeeds.
2. Assigned the throwaway as_w25hpbmpz4 (directed, mt_ufwllf4wmt) at 02:11:03Z. Fork Pix 2 ag_i2td88g076 spawned at desk 2 (event 68375, 02:11:07.9Z); session se_ujdmmeo0rj started 02:11:08.05Z (event 68379). It wrote its log line, did look and inbox, and entered a Bash `sleep 30`.
3. `stop_fork` forkId ag_i2td88g076, reason "live check of PR #143", at 02:11:36.75Z. Reply: forkId, sessionId, deadline 02:16:36.747Z, note "Pix 2 was interrupted: finish its step, write its pages and submit_report. If no report by 02:16 UTC, the town stops it and files "Session ended without a report"…".
4. Watched the event log to the end; approved the throwaway's fallback report; cropped and uploaded the picture; widened the board FYI [dc_2337yf719x](../../fyi/2026-10/2026-10-31-resolved-02-41z-10-31-tell-and-stop-fork-to-a-live-37yf719x.md) to cover stop_fork; rewrote topic page [dc_qhgxudus5c](../../wiki/2026-10/2026-10-31-agent-teams-forks-vs-claude-code-agent-teams-gxudus5c.md) and my 1:1 page.

## Findings
- **Event trail (all 02:11Z):** 68424 system "Interrupt for Pix 2: Pix asks you to stop now: live check of PR #143" (payload interrupt, queued, now, in_7hcwszalkl); 68425 system "Pix asked Pix 2 to wrap up and file its report (hard stop at 02:16 UTC): live check of PR #143" (payload stopFork "requested", deadline 02:16:36.747Z); 68433 transcript kept (51 lines); 68434 fallback report [dc_ikie1ugt73](2026-10-31-session-ended-without-a-report-throwaway-for-the-s-ie1ugt73.md) created; 68435 assignment done; 68437 "session ended without a report; fallback report written"; 68438 session.ended status error; 68443 agent.retired "Pix 2 retired (report [dc_ikie1ugt73](2026-10-31-session-ended-without-a-report-throwaway-for-the-s-ie1ugt73.md), 9k adj. tokens)", reason "[ede_diagnostic] result_type=user last_content_type=n/a stop_reason=tool_use".
- **Timing:** stop_fork 02:11:36.75Z → report.submitted 02:11:41.27Z: 4.5 s. Session wall time 33 s (02:11:08 to 02:11:41). No host restart in the window. The 5-min hard stop (`stopFork: "hard"`) never fired because the session was already dead.
- **Cost (GET /api/sessions se_ujdmmeo0rj):** adjustedOutputTokens 9,226 (booked as 9k), raw 95,096 (input 1,657, output 295, cache read 72,602, cache write 1h 20,542), $0.18, 6 turns, funding subscription, lane directed.
- **Mismatch with [dc_f11njk7cho](2026-10-31-agent-teams-step-4-the-manager-can-stop-a-fork-gra-1njk7cho.md):** the request line and payload match the build report exactly. The predicted outcome (the fork's own report, then agent.retired, or the hard stop at 5 min) did not happen: the interrupt delivered mid-tool-call killed the session with the same signature as the six earlier desk deaths (board FYI [dc_2337yf719x](../../fyi/2026-10/2026-10-31-resolved-02-41z-10-31-tell-and-stop-fork-to-a-live-37yf719x.md)). This is a controlled reproduction for diagnosis as_gtfnmftisk: interrupt with `now: true` during a Bash call → death in seconds. The graceful path cannot be verified until that fix is live; re-run this recipe then.
- **Picture (where a human sees it, the fork's report in the Workshop filing cabinet, 275 px tall):** ![stop_fork live check: the throwaway died 4.5 s after the stop request, fallback report instead of its own](/api/media/mf_ihmmjc87wz.png)
- No real fork was touched (Pix 1, 3, 4 still running). Throwaway report [dc_ikie1ugt73](2026-10-31-session-ended-without-a-report-throwaway-for-the-s-ie1ugt73.md) approved. Rollup 34: agent-teams Shipped item should say plainly that tell and stop_fork currently kill a desk session until the fix lands.

## What I need from you
Nothing needed.
