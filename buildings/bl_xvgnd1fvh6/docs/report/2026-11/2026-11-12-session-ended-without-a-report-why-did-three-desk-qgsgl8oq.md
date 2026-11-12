---
id: "dc_olqgsgl8oq"
type: "report"
state: "building"
title: "Session ended without a report: Why did three desk sessions die with desk exited -1 between 17:10 and 17:56Z today?"
authorId: "ag_1ye4nm1sb9"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "redirect"
decisionNote: "Find why four desk sessions died with \"desk exited -1\" today and fix the cause. The deaths: Workshop desk Pix 2 at 17:50Z (as_0rk272gsne, 131k tokens) and again 18:13:56Z (se_yzm7229zkz, as_wnztwvxq7f, 0 tokens); Pix 1's desk at 17:56Z (se_0oj7ljgofe, 32k); Prod desk Cleo 1 at ~17:10Z, and the first investigation session itself (se_h0z2jxx7gf, as_n4ffhi3ev4, 46k, ended 18:25Z). Code read so far (cite and confirm): -1 comes from packages/runtime/src/desk/fly.ts:262 (five consecutive failed exec polls, each a 20 s Fly exec), fly.ts:240-242 (abort) or sandbox.ts:157-159 (writeSecretFile or the launch exec threw); a -1 without a kill is treated as a frozen guest and sandbox.ts:164-170 calls stopNow, so the next ensure() restarts the Machine (sandbox.ts:113,134; fly.ts:177-190). Lead to test first: every desk Machine is created with init cmd `sleep maxLifetimeSec` = 6 h (fly.ts:56,123, restart policy \"no\"), and index.ts:308 says Machines stop themselves after that lifetime. If a Machine was started ~6 h before each death (about 11:10-12:25Z, e.g. by a server restart or image redeploy then), the sleep ran out mid-session, the guest went away, polls failed and the session died with -1 at whatever token count it had reached; the 0-token death at 18:13Z would then be a session that started on a Machine still stopping or not yet reachable. Check with the Fly Machines API (FLY_API_TOKEN/FLY_APP on your desk; GET /v1/apps/$FLY_APP/machines/<id>/events and the machine's updated_at / started events): for each dead desk, when was the Machine last started and when did it stop, and does stop time match the death time and start time + 6 h? Also read the server log lines \"[sandbox desk-...] process ended (exit -1)\" and \"Desk ... stopped after exec failure\" events (world events, type system, payload.deskStopped) for the exact times. If the lifetime is the cause, fix it in the runtime (not the Machine's lifetime alone): e.g. in SandboxBackend.ensure() or FlyApi.start(), when a found started Machine is older than maxLifetimeSec minus a safety margin (say 4.5 h of uptime, read from the Machine's events or a /proc/uptime exec), stop and start it before the session begins; and/or raise maxLifetimeSec so a session can never straddle it. Add a test in packages/runtime/test for the new behaviour. If the cause is something else (Fly host maintenance, OOM, the API returning errors), say so with the evidence and fix that instead. Open a PR, run npm run check --fast, merge when green, do not call redeploy. Keep your session short and file your report early if the desk feels slow: the last investigator died the same way. Report: cause with evidence (machine ids, start/stop times from Fly events), the PR, and whether the Workshop's Pix 2 Machine needs a recreate (tell Pix ag_mh0qidzgw6 if it does)."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-12T18:26:31.211Z"
sessionId: "se_h0z2jxx7gf"
assignmentId: "as_n4ffhi3ev4"
costUsd: 0
tokens: 46194
turns: 0
createdAt: "2026-11-12T18:25:06.395Z"
updatedAt: "2026-11-12T18:26:31.211Z"
---
## What I did
Assignment: Why did three desk sessions die with desk exited -1 between 17:10 and 17:56Z today?. The session ended without `submit_report` (error: desk exited -1); this is a fallback report written by the runtime.

## Findings
(no final message)

## What I need from you
Nothing needed unless the task still matters: the session failed before it could work, so re-assign it once the cause above is fixed.

