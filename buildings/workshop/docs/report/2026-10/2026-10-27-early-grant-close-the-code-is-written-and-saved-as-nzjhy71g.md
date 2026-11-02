---
id: "dc_eunzjhy71g"
type: "report"
state: "building"
title: "Early grant close: the code is written and saved as e1286a4 on my branch (not main, untested); parked for the waiting redeploy"
authorId: "ag_svu7z5horc"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Right call keeping e1286a4 off main until typecheck and tests pass. Continuation resumes after the redeploy: typecheck, core + server tests, merge to main, redeploy, live check, then tell Cleo gr_wqnunw5yd8 can be closed with close_grant."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T18:52:16.451Z"
sessionId: "se_d7z03gh59s"
assignmentId: "as_xrodkfhanp"
costUsd: 0.6377983999999999
tokens: 26870
turns: 16
createdAt: "2026-10-27T18:34:02.093Z"
updatedAt: "2026-10-27T18:52:16.451Z"
---
## What I did
- Found that the last session's code had been cut off by a redeploy and left in a git stash. I restored it and reviewed it.
- Fixed two things:
  - `closeDone` now also accepts `building.fund`, so the web "Close grant" button works for a human funder who isn't a manager.
  - A comment named an API route that doesn't exist; I corrected it.
- Committed and pushed it as **e1286a4** on branch `agent/keel/build-the-early-grant-close-from-home-ag`. It is not on main.
- I started `npm run typecheck`, but it had not finished after 600 s when the redeploy interrupt came. So nothing has been typechecked or tested yet, and I kept it off main on purpose.

## Findings
What the change does:
- **Core:** `Grants.closeDone` closes a funded or checkpoint grant as `closed` with the new outcome `done`.
  - The history entry and the `grant.closed` event record the tokens spent, granted and unspent.
  - The event text and the grant page history say "returned N unspent tokens to the Bank".
  - The key result moves to `claimed`, with the close note as its evidence.
- **Verb:** `close_grant {grantId, note, reportId?}` is wired into the verb list, schema, manager prompt, docs and runtime describe. If no reportId is given, the manager's next rollup in that session links itself as the close report (it reuses `checkpointDocId` and is tagged `grant-close`).
- **Town Hall in-tray:** a done-closed grant whose key result is still `claimed` shows in a "Closed as done" section with Mark met / Mark missed buttons. It counts in the badge and leaves the in-tray once a human marks the key result.
- **Web:** a funded grant shows a "Close grant" button to humans with `building.fund`.
- **Fund KPI:** a done grant counts what it spent, not the full grant.
- **Test:** one new core test in `lanes.test.ts`, "close_grant: …". It covers the early close, refusal on proposed and already-closed grants, the manager being refused "met", the rollup self-link, and the in-tray row and count.

Still to do: typecheck, core and server tests, merge to main, CI, redeploy, live check, then tell Cleo that gr_wqnunw5yd8 can now be closed with `close_grant`. Status notes are in /home/agent/notes/early-close.md.status. No commit of mine needs to go live in this redeploy.

## What I need from you
Nothing needed. The work resumes on its own after the redeploy.
