---
id: "dc_t1aisohw4u"
type: "report"
state: "building"
title: "Manager-wake audit: only a fresh in-tray report or an open 1:1 wakes a manager; grant funded, checkpoint decided and new KR wake nothing; fix is a town-written in-tray row in Grants.decide() (~25 lines), built once the Workshop grant is funded"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Audit complete and filed (dc_362tfcb7qi). Build of the Grants.decide() in-tray row waits for the Workshop grant to be funded, per decision 3."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-25T16:45:49.992Z"
sessionId: "se_3khsiaxxp4"
assignmentId: "as_isxtyps3eq"
costUsd: 2.9354903000000006
tokens: 28035
turns: 30
createdAt: "2026-10-25T16:45:09.474Z"
updatedAt: "2026-10-25T16:45:49.992Z"
---
## What I did

Read the runtime dispatcher and manager wake logic (runtime/src/index.ts, runtime/src/manage.ts), the grant desk (core/grants.ts), waits and the lane gate (core/waits.ts, core/lanes.ts), in-tray routing (core/domain.ts) and the prompts, all on main 4d6a941 (live per /api/health). Checked the live Workshop grant board and Town Hall in-tray. Filed the full table and the proposed change as a building note, [dc_362tfcb7qi](../../note/2026-10/2026-10-25-what-wakes-a-manager-today-and-the-smallest-change-2tfcb7qi.md), and told Pix. No code change (decision 3 says build only after the grant is funded).

## Findings

**What wakes a manager's team-lead (manage) session today**: exactly one condition, checked in `wakeManager` (manage.ts:88): an unoffered pending report in `intrayOf(building)`, or an open 1:1. It is evaluated on `doc.created` of a report (index.ts:265), on 1:1 meeting events (index.ts:261-263) and on every 5-s tick (index.ts:387). Town-hall and building meetings run the manager as facilitator or in a meeting-reply session, not a manage session. Parked work (`checkWaits`) and held grant-lane work (lane gate, lanes.ts:59-65) start the assignee's work session, not the manager's. The one grant event that does reach the manager is the 50%/100% checkpoint crossing, which creates a front-of-queue "Write the checkpoint" assignment (grants.ts:243).

**The three KR3 triggers wake nothing**:
- Grant funded / continued / adjusted: all emit `grant.funded` (grants.ts:151, 175, 186). Not handled by `onEvent`, no inbox message, no wake. The manager sees the funding only in its next session's grants block, whenever that session happens for another reason.
- Checkpoint decided: continue/adjust are the case above; cut emits `grant.closed` plus an inbox message (`notifyManager`, grants.ts:193), and inbox messages wake nothing. A human approving the checkpoint rollup via `review` only flips `doc.decision`.
- New KR: key results are replaced wholesale by `setKeyResults` (grants.ts:310) on create/update and on fund/counter/adjust, with no event at all (`kr.updated` fires only on a status change). Counter and reject also only send an inbox message.

Workaround available now: a manager may `assign` grant-lane work against a *proposed* grant's KRs (lanes.ts does not check status); the gate holds it "grant not funded yet" and the scheduler releases it on the first tick after funding. The residents resume; the manager is not told.

**Smallest change that closes the gap (recommended, in [dc_362tfcb7qi](../../note/2026-10/2026-10-25-what-wakes-a-manager-today-and-the-smallest-change-2tfcb7qi.md) §3)**: in `Grants.decide()` (grants.ts:134), after each of the six human actions, write a town-authored pending `report` into the building in-tray (author = manager agent, tags `grant-decision` + action, body opens "Written by the town", lists the grant's KRs and what to do). It rides the existing path: `doc.created` → `wakeManagers` → manage session (or streamed into the live one); not tagged `rollup` so it stays in the building; the manager may `review` it thanks to PR #51; it survives restarts and shows in the in-tray UI. Precedent: the `wait-expired` reports in waits.ts. About 25 lines in core/grants.ts plus one core test, no runtime or schema change. Latency is immediate, subject to the usual gate (manager idle, free slot, not draining), so it meets "within one session cycle". An in-memory runtime notice queue was considered and rejected: 40-60 lines, lost on restart, invisible to humans.

Also for decision 4 (as_6pacj1qc9n, queued for me): `Building.budgetMode` defaults to `"open"` (schema/src/index.ts:165), so that change is a one-line default plus web mock fixtures.

## What I need from you

Nothing needed. Fund or counter the Workshop grant gr_jqsqra0dlx in the Town Hall in-tray; the fix above gets built once it is funded.
