---
id: "dc_30oz0bnnob"
type: "report"
state: "building"
title: "Waiting design: re-pull after drain + live sha now, then assignments that wait on a dependency (doc dc_0sbtispjk3)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_0sbtispjk3","dc_fhek8huw41","dc_7nqgp6hw4g","dc_tcsilvtkdu","dc_ebiafveus2","dc_x8sufqw7cd","dc_rvwdvfhbkz","dc_ev7qckfr1h"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "sgtm on all. for P2 sure, let's allow resuming automatically"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T20:01:50.186Z"
sessionId: "se_h3yr1sepn5"
assignmentId: "as_iro0bhk4nq"
costUsd: 1.2826527999999997
tokens: 68376
turns: 33
createdAt: "2026-10-20T19:56:45.224Z"
updatedAt: "2026-10-20T20:01:50.187Z"
---
## What I did
I read `runtime/redeploy.ts`, `desk/src/run.ts` and `core/domain.ts` on main @ 8842a21. I then measured the problem against today's workshop event log (6,002 events) and all 102 workshop reports. The full design is in **[dc_0sbtispjk3](../../article/2026-10/2026-10-20-design-how-agents-wait-on-in-progress-work-and-pic-btispjk3.md)** in the filing cabinet. This was report only, so I made no code changes and opened no PR.

## Findings
**Where waiting bites today:**
- **Redeploys miss the very pushes they wait for.** A redeploy pulls main first and then drains for 3–13 min, waiting on the agents who are about to push. In 4 of today's 5 drained redeploys, commits made during the drain were left out of the restart: 9 commits in total, all by agents the drain was waiting on. My refused 8842a21 is one of them. Each one then needed "one more redeploy".
- **Nobody could tell what was live.** Lena's 19:48:57 redeploy actually shipped the Bank at 19:49:09. The 19:50 standup still thought it wasn't live and ordered two redeploys that each pulled 0 commits. `/api/health` doesn't report the running commit.
- **Waiting inside a session silently ends it.** The desk host ends the session as soon as a turn ends, so background timers and Monitors never wake the agent. Four of the last six fallback reports are agents who tried to wait this way (Sage ×2, Pix, Lena; 25–83 turns, $6.96 in total). Their work resumed only when the next standup re-assigned it.
- **The scheduler ignores dependencies.** The 19:53 decisions "After the redeploy, Lena…" and "Once the Bank is live, Sage…" both started at 19:53:16, before the redeploy was even requested.
- **"Once X lands" notes need a human to relay them.** 19 of the 102 reports contain notes like this.

**Options compared:**
- **Queued redeploy:** fixes the missed pushes, but only for redeploys.
- **In-session waiters:** a trap. They die on restart and deadlock with the drain, which is waiting for the same session.
- **Waiters that wake the requester:** to respect "nothing continues without a decision", this collapses into the next option.
- **Assignments that unblock on a dependency:** durable in SQLite, visible in the UI, and the work was already decided by someone.

**Recommendation, phased:**
- **P0** (1 small session): redeploy pulls again after the drain. A request during a run joins it instead of being refused. `/api/health` and the "finished" event carry the live sha. Agents' prompts say they can't wait inside a session.
- **P1** (about 2 sessions): `Assignment.waitFor`. A wait can be on a deploy containing a given commit, another assignment finishing, a report getting a decision, or a time. The scheduler skips the assignment until the wait is met. Waits are set wherever decisions are already made (`assign`, meeting `decide`, Continue/Redirect). An unmet wait expires after 24 h and lands in the in-tray. This uses the same pattern as visitor offers.
- **P2** (about 1 session): `submit_report` with `resumeWhen` parks an agent's own work. The continuation would wait for its condition, with Stop/Redirect in the in-tray, at most 3 resumes, and the same 24 h expiry.
- **Not now:** watching git for pushes, and blocking waits inside a session.

## What I need from you
Decide whether parked work (P2) may resume automatically once its condition is met, without a fresh decision on the parked report. P0 and P1 don't depend on that, so they can be assigned now.

## Reply from Mitchell (2026-10-20 16:01)

sgtm on all. for P2 sure, let's allow resuming automatically

