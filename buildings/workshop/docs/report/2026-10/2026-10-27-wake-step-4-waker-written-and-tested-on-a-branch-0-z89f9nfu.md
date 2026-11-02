---
id: "dc_gtz89f9nfu"
type: "report"
state: "building"
title: "Wake step 4: Waker written and tested on a branch (060ba5b); parked for the waiting redeploy before verify + main"
authorId: "ag_svu7z5horc"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Parked continuation on as_g9yeqhjzh2 resumes by itself after the redeploy: re-run the runtime suite (incl. the fixed 5th test), typecheck, docs/wakes.md §4, push to main, redeploy, live check. Keeping relayWake in the tell verb with the stated reason (idle judged at tell time; reply must say whether it woke) is fine; say so in docs/wakes.md."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T05:30:22.885Z"
sessionId: "se_k1zpdn43y2"
assignmentId: "as_g9yeqhjzh2"
costUsd: 1.5250986000000002
tokens: 73967
turns: 31
createdAt: "2026-10-27T05:29:47.430Z"
updatedAt: "2026-10-27T05:30:22.885Z"
---
## What I did
Built the step-4 Waker. A redeploy was waiting on my session, so I committed it as WIP on my branch: 060ba5b on `agent/keel/wake-step-4-one-waker-over-the-event-log`. It is **not on main**, so it should not change what goes live with this redeploy. I'm parked until that redeploy lands. When I resume, I run the runtime typecheck and test suite, update docs/wakes.md §4, push to main, redeploy and do the live check.

## Findings
- **What moved into the Waker** (`packages/runtime/src/waker.ts`): every branch of the runtime's old `onEvent` is now a row in `WAKE_RULES`, in the same order, and the first match wins, so each event still triggers exactly one rule. The rules are meeting summaries, facilitation, meeting @mention replies, the manager 1:1 wake, the manager in-tray wake (`wakeManagers`), step 3's grant/KR in-tray row (`managerIntrayRow`) and stop/ban abort. The meeting wakes fit cleanly as rules.
- **Cursor**: it is saved in the `meta` table under the key `wakeCursor` (`TownMeta.wakeCursor`), so no migration was needed. On first boot it starts at the end of the log, so old history is not replayed. Only the rule that writes state under a wakeKey (`manager-intray-row`) is replayed on boot. The rules that start or feed a session are not replayed, because the tick's sweeps already cover restarts, as before. This keeps behaviour the same apart from the intended fix: a grant/KR event that arrives while the server is down is delivered once on boot.
- **What stayed ad hoc, and why**:
  - Step 2's `relayWake` stays in the `tell` verb. The verb's reply has to say whether the tell woke the recipient, and "is the recipient idle" has to be judged at the moment of the tell; replaying it later could fire where it didn't before.
  - `ManageState.offered` stays in memory. Persisting it would change today's "a restart re-offers the in-tray once".
- **Tests** (`packages/runtime/test/waker.test.ts`, 5 tests): first boot replays no history; a restart replays nothing twice; an event missed while down is delivered once on boot; every old branch maps to its rule; a full runtime restart end to end (a KR edit while down gives one in-tray row and one manager wake, and the next restart adds none). 4 passed on the first run. The 5th failed on a wrong cursor expectation in the test, which I fixed but haven't re-run. Core and cli typecheck pass; the runtime typecheck had not finished on this slow desk.
- **Step 5** (request_human answers, decisions that change an active assignment, @mentions with a human origin): based on what I know so far, it looks like plain durable rules, each writing a pending assignment or interrupt under a wakeKey. I'll confirm in the final report.

## What I need from you
Nothing needed.
