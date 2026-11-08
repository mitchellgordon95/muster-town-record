---
id: "dc_u5p7xy0t9v"
type: "report"
state: "building"
title: "Routing 4-hour soak: no misfires. 0 manager work sessions, 14 building-queue rows (13 run, 1 held correctly), 3 wake rows (0 pending, 0 dropped), 0 errors"
authorId: "ag_5xxq41agg2"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Soak clean: 0 manager work sessions, 14 queue rows routed right (13 run, 1 held at checkpoint), 3 wake rows all landed, 0 errors. Folding into the routing rollup."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-08T08:02:20.159Z"
sessionId: "se_85rv9u56w6"
assignmentId: "as_a7cms3vzqp"
costUsd: 1.1039215
tokens: 55196
turns: 23
createdAt: "2026-11-08T08:02:09.622Z"
updatedAt: "2026-11-08T08:02:20.159Z"
---
## What I did
I read every live event from 03:53:40Z (step 1 live) to 08:00:24Z, events 140691–141644, and checked that all 954 IDs were consecutive. I also read GET /api/buildings/<id>/intray and /queue for all 7 buildings and /api/town. I changed nothing. I rewrote the topic page "Work routing" ([dc_ktzj41hv8x](../../wiki/2026-11/2026-11-05-work-routing-zj41hv8x.md)) with the result.

## Findings
**Every manager is a forking manager.** The 7 non-Town-Hall managers are all residents, so all 7 count as forking managers (domain.ts:338).

1. **Manager work sessions: 0.** 31 sessions started in the window:
   - 16 were manager sessions: Mara 14, Cleo 2, Pix 1. Every one had `purpose: "manage"` and `assignmentId: null`.
   - 15 were fork work sessions: Mara's forks 13, Cleo's 2.
   - 1 was the Secretary's retainer, which runs in Town Hall and isn't a manager session.
2. **assignment.created naming a forking manager: 14, all `queue: "building"`.** Mara 12, Cleo 1, Pix 1. The 15th was the Secretary's, `queue: agent`, and is not a manager's.
   - **13 were run by a fork**, each with an `active` status event from a fork agent. The 13th is this session.
   - **1 is held, and should be:** Workshop as_62lpwynu0z (gr_bwm0iz7rwl step 3b) shows "held: grant at checkpoint".
   - Every pending row on all 7 queues shows agentName "next free desk". No pending row belongs to a manager's own queue.
   - 0 `queueRepair` events, so the boot repair at the step-2 restart found nothing left to move.
3. **Wake rows: 3 written, 0 pending, 0 dropped by the caps.** All 3 are in our building: [dc_fwa27srwkj](2026-11-08-message-from-mitchell-via-mara-1-live-check-2-prob-a27srwkj.md) (wake:relay), [dc_u7ayc5tavx](2026-11-08-mentioned-by-mara-1-for-mitchell-note-live-check-2-ayc5tavx.md) and [dc_n6bk8zf1oq](2026-11-08-mentioned-by-mara-1-for-mitchell-report-live-check-bk8zf1oq.md) (wake:mention).
   - Mara approved all 3 (04:56:48Z, 04:56:50Z, 07:02:36Z). All 7 in-trays have 0 pending rows now.
   - 8 agent.told / agent.mentioned events in total. 3 carried an origin (1 hop, origin at 03:24Z, well inside 24 h), and each made exactly 1 row.
   - The other 5 had `origin: null`: 3 tells to Pix, 1 tell and 1 mention to Mara. Without an origin they went to the inbox only, which is the design. All 5 came from sessions that started before #397 went live (04:07Z–04:29Z). Every tell or mention after 04:49Z carried an origin.
   - 0 grant countered/rejected events in the window.
   - These drops make no event (wakes.ts returns null), so I counted them from the events' `payload.origin`.
4. **Error or warning events about wakes, intray or createAssignment: 0.** The 87 system events are 3 CI redeploys (3320f44 → 5f6571f → b9b1490 → 300072b), session adoptions, kept transcripts and in-tray-session-ended lines. Two system reports in the window aren't routing faults:
   - [dc_osu85j8oyx](2026-11-08-session-ended-without-a-report-work-routing-step-3-u85j8oyx.md): a fork ended without a report, and the fallback report was written.
   - [dc_vjvw1ecklh](../../../../workshop/docs/report/2026-11/2026-11-08-pix-s-assignment-never-unblocked-first-live-reset-vw1ecklh.md): Pix's wait expired after 24 h.

**One oddity, not routing:** Mara's 07:02:31Z approve note on [dc_ffmczdp76j](2026-11-08-gr-7op2v8fjcl-midpoint-no-red-main-since-ed953de-w-mczdp76j.md) has leaked tool-call markup in it ("…</note></invoke><invoke name="mcp__town__read">…"), and its text describes a different doc ([dc_tt7r3npm6y](2026-11-08-live-check-2-passed-directed-continuation-s-tell-a-7r3npm6y.md)'s mention row). The decision itself (approve) is right; only the note text is garbled.

Verdict: the restructure ran 4 h town-wide without a misfire. This is ready to fold into the rollup of steps 2+3, #397 and live check 2.

## What I need from you
Nothing needed.
