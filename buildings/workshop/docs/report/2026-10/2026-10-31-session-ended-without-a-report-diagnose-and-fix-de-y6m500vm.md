---
id: "dc_ary6m500vm"
type: "report"
state: "building"
title: "Session ended without a report: Diagnose and fix: desk sessions die mid-tool-call on every host restart (4 deaths across the 01:59Z and ~02:03Z restarts); start from Pix 2's queued_turn_count lead"
authorId: "ag_wlk1ooccbm"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "redirect"
decisionNote: "Diagnose and fix (third attempt, after Pix 3's as_ak5sacymxe lands): desk sessions die mid-tool-call on every host restart. Five deaths tonight, all with \"[ede_diagnostic] result_type=user last_content_type=n/a stop_reason=tool_use\" and the runtime's fallback report: se_z3wxpka8sv and se_vunrohrww0 at the 01:59:22Z restart (d42d458), se_tn0gp7c9ye and se_ngxe1pbsk9 at the 02:02:55Z restart (89fd8a8), and se_bdg0zvmebg (the diagnosis itself, Pix 2, as_1onb010x05) at 02:06:29Z (confirm from GET /api/health startedAt / the event log whether a restart to 2f38712, Nell's PR #147, happened then; if there was no restart the deaths are not restart-bound and that changes the diagnosis). Pix 1's se_2iq47zjp5y, in long Bash calls, survived every restart: the deaths look tied to a town (MCP) call in flight when the host goes down.\n\nFIRST read Pix 3's report for as_ak5sacymxe (it was fixing packages/desk/src/run.ts: an aborted/injected-turn path with eagerSdk tests, likely the same mechanism as Pix 2's lead \"does the real SDK ever send the queued_turn_count field the desk relies on\"). If Pix 3's report says its fix covers the restart deaths and the commit is live, do only the live check: GET /api/health commit, then confirm from the event log that the next restart after that commit killed no desk session (or, if none has happened, say so and stop with verdict stop). Otherwise pick up where Pix 2 and Pix 3 stopped (Pix 2's transcripts: se_ngxe1pbsk9 and se_bdg0zvmebg; the transcript store is on the attached page), and deliver: (1) the exact cause in plain words; (2) a fix PR on main if it is our code: desk sessions survive a restart, or at minimum a session killed mid-call re-queues its assignment instead of filing a fallback report; (3) if it is an SDK limitation, the evidence and the cheapest mitigation. Merge your own green PR, queue a plain redeploy, say which commit should be live, park with resumeWhen {deploy: sha} and live-check.\n\nProtect yourself: do the whole investigation in Bash on the local checkout and node_modules SDK source; make town calls only to write the wiki page and the log early (one log line as soon as you have the cause) and to submit the report, so a restart mid-session loses little. If a redeploy is queued when you start, say so in the report. Open the report with one plain sentence on what Mitchell can now rely on."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T02:08:10.694Z"
sessionId: "se_bdg0zvmebg"
assignmentId: "as_1onb010x05"
costUsd: 0.45624679999999995
tokens: 22812
turns: 16
createdAt: "2026-10-31T02:06:29.315Z"
updatedAt: "2026-10-31T02:08:10.694Z"
---
## What I did
Assignment: Diagnose and fix: desk sessions die mid-tool-call on every host restart (4 deaths across the 01:59Z and ~02:03Z restarts); start from Pix 2's queued_turn_count lead. The session ended without `submit_report` (error: [ede_diagnostic] result_type=user last_content_type=n/a stop_reason=tool_use); this is a fallback report written by the runtime.

## Findings
Tracing where the SDK's CLI builds the `[ede_diagnostic]` message, to see what makes it end a turn.

## What I need from you
Nothing needed unless the task still matters: the session failed before it could work, so re-assign it once the cause above is fixed.

