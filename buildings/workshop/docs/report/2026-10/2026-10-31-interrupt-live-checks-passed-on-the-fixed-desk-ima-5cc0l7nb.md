---
id: "dc_8v5cc0l7nb"
type: "report"
state: "building"
title: "Interrupt live checks passed on the fixed desk image: a tell no longer kills a fork, and stop_fork gets the fork's own report in 8 s; board FYI dc_2337yf719x resolved"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_19rkc8muf0","dc_nuqor7523e","dc_0g9dpfedg9","dc_d7krdc8ehb","dc_2jki6d35ku","dc_2337yf719x","dc_jkf959uvlq","dc_qhgxudus5c"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Both interrupt live checks passed on the fixed desk image (tell survived, stop_fork → own report in 8 s). FYI dc_2337yf719x resolved. 5-min hard stop stays untested; step 3 proof waits on Mitchell's 1:1 question."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T02:44:08.706Z"
sessionId: "se_bvtoao6gjd"
assignmentId: "as_mcu7gbwcf6"
costUsd: 3.1871032
tokens: 63742
turns: 38
createdAt: "2026-10-31T02:43:50.849Z"
updatedAt: "2026-10-31T02:44:08.706Z"
---
**What Mitchell can now rely on:** a `tell` to a live fork reaches it as an interrupt and the fork keeps working, and `stop_fork` makes a fork wrap up and file its own report within seconds (8 s in the live check), with no fallback "Session ended without a report". The desk-death rule on the Workshop board is lifted.

## What I did
Steps as the manager (forks can't assign or stop_fork): read Pix 3's report [dc_nuqor7523e](2026-10-31-tell-interrupt-check-not-run-no-fork-on-the-fixed-qor7523e.md) (no target found, no tell sent, so I ran the tell check too). GET /api/health: 85b106b, started 02:38:04Z, contains 1df29a4. My own desk is on the fixed image (`grep -c pushedSinceResult run.ts` = 6, file dated 02:23:59Z). Assigned the throwaway as_oa7b9l670k (directed, mt_ufwllf4wmt); fork Pix 2 ag_ac5xhir3dq started session se_b20zg7exmd on desk 1 at 02:38:15Z and logged run.ts count 6. Sent the tell mid-wait, checked 2 min later, then stop_fork mid-wait with reason "live check of PR #143", watched the event log, approved its report [dc_19rkc8muf0](2026-10-31-throwaway-interrupt-live-checks-rkc8muf0.md). Rewrote board FYI [dc_2337yf719x](../../fyi/2026-10/2026-10-31-resolved-02-41z-10-31-tell-and-stop-fork-to-a-live-37yf719x.md) in place as RESOLVED (the unpublish verb only covers Town Hall notes), topic pages [dc_jkf959uvlq](../../wiki/2026-10/2026-10-31-desk-sessions-dying-mid-call-interrupt-now-f959uvlq.md) and [dc_qhgxudus5c](../../wiki/2026-10/2026-10-31-agent-teams-forks-vs-claude-code-agent-teams-gxudus5c.md), my wiki pages dc_u45t9giud5 and dc_4tnacz1i0v, one log line. Pix 1 (as_jtkc86p4u2, the step 8 live check) ran alongside, untouched.

## Findings
- **Tell check (passed):** interrupt event 69349 "Interrupt for Pix 2: Pix told you…" at 02:38:34.887Z, while the fork was inside a Bash until-loop wait. The fork saw it at 02:38:38Z, carried on looping (02:39:17, 02:39:49, 02:40:21Z); GET /api/sessions/se_b20zg7exmd was still `running` at 02:40:43Z. No session.ended, no "[ede_diagnostic]".
- **stop_fork check (passed):** request 02:40:47.882Z (events 69392 interrupt, 69393 stopFork requested, deadline 02:45:47Z), again mid-Bash wait. The fork's OWN report [dc_19rkc8muf0](2026-10-31-throwaway-interrupt-live-checks-rkc8muf0.md) at 02:40:55.924Z (8.0 s after the request), assignment done 02:40:55.9Z, transcript kept (165 lines), session.ended status `done` 02:40:59.565Z, agent.retired 02:41:00.217Z. The 5-min hard stop was never reached. The earlier check on the old image ([dc_d7krdc8ehb](2026-10-31-stop-fork-live-checked-on-2f38712-the-stop-interru-krdc8ehb.md)) had died in 4.5 s with a fallback report; that path is fixed.
- **Cost:** 24,255 adj. tokens ($0.49), 3 turns, 2 min 44 s wall, subscription, lane directed.
- **Known and accepted behaviour:** the interrupt still cuts the in-flight tool call (the fork's wait ended early both times), and the desk resends the interrupt text once ("Resent: your last turn was cut off"), so the fork sees it twice. Also: the desk's tool hook blocks a plain `sleep 30`; the throwaway used an until-loop.
- **Still untested:** the 5-min hard stop (`stopFork: "hard"`), which only a fork that ignores the request would hit. Step 3's proof (manage session reads main) still needs Mitchell's 1:1 question.
- **Picture for rollup 34 (the throwaway's report in the Workshop filing cabinet, 300 px tall):** ![The throwaway's own report: tell survived, stop_fork to own report in 8 s, no fallback](/api/media/mf_9v3hrw5zbd.png)

## What I need from you
Nothing needed.
