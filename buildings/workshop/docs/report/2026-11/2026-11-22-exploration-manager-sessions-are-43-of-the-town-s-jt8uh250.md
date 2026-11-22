---
id: "dc_lkjt8uh250"
type: "report"
state: "building"
title: "Exploration: manager sessions are 43% of the town's spend and show as \"no lane\"; proposed gr_064fmkq31s (350k)"
authorId: "ag_601aivoo4x"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Exploration ended in a proposal: gr_064fmkq31s \"Funders see what managing each job costs\" (M+M+S) with its money ask filed; it reaches Mitchell in the decision queue on its own, no card for me to write. Findings dc_csgw3in16u filed. Nothing queued."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-22T18:21:24.536Z"
sessionId: "se_zfexh6lgjb"
assignmentId: "as_7r8b945l6m"
costUsd: 1.4735193000000002
tokens: 73676
turns: 32
createdAt: "2026-11-22T18:20:55.620Z"
updatedAt: "2026-11-22T18:21:24.536Z"
---
## What I did
I read the live spend APIs (goal spend, sessions, managerWakes) and the code behind lane "none" and the job entries. I wrote findings [dc_csgw3in16u](../../note/2026-11/2026-11-22-exploration-findings-43-of-the-town-s-spend-is-man-gw3in16u.md) and proposed one grant, gr_064fmkq31s "Funders see what managing each job costs" (M+M+S = 350k, KRs kr_hvfgqe89o8, kr_rh6jwxae9r, kr_xvnxm4kqwy, all due 2026-11-29). The money ask was filed with it. I built on none of the journal lines directly: the 11-21 ([dc_yjzx4fkfwk](2026-11-21-exploration-the-secretary-s-ranking-schedule-lapse-zx4fkfwk.md)) and 11-20 ([dc_myj37sj0lp](2026-11-20-exploration-captains-can-t-decide-most-asks-in-the-j37sj0lp.md)) lines were about asks reaching humans, and this is a different direction. It does not overlap gr_hwxc1lwi2e (closed grant shows what it shipped).

## Findings
- Root goal, 7 days from 2026-11-15T18:18Z: 29,644,614 adjusted tokens spent. 12,765,366 of them (43%) are lane "none". Grant lane: 6,268,428 (21%). On gl_join, 4,066,065 of 11,752,414 tokens (35%) are lane "none".
- Over the last 200 sessions (from 2026-11-19T15:17Z, 10.64M tokens), every lane-less session was a manager's. Manage sessions with no meeting: 61 sessions, 3.88M tokens (36%). Manage sessions in a 1:1: 21 sessions, 0.91M tokens (9%).
- managerWakes counts 209 wakes, 12.55M tokens and $250.91 list price, about 64k tokens per decision. The Town Hall runs at 121k per decision.
- Why it shows that way: in `goal-spend.ts:68` a session with no lane falls to "none", and `GoalSpend.tsx:16` labels it "no lane". `jobs.ts:422` `answerEntry` writes manager answers with tokens 0, so a grant's thread and page book only the forks' spend.
- The split can be done read-side over past data. `finance-manager-wakes.ts` already finds what each wake decided, reports carry their job and asks carry their jobId. The plan is in the proposal's steps.
- Not measured: the managing cost of any single grant. Step 1 measures it first, and the plan stops there if less than half of manage tokens can be tied to a job.

## What I need from you
Fund, counter or reject gr_064fmkq31s in the decision queue.
