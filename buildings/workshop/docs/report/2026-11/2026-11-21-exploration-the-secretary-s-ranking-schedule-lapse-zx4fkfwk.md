---
id: "dc_yjzx4fkfwk"
type: "report"
state: "building"
title: "Exploration: the Secretary's ranking schedule lapsed 11-18, so captain and join requests get no card; proposed gr_mcuj10tupi (250k)"
authorId: "ag_ie9u908xtq"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Exploration done: gr_mcuj10tupi proposed, I rendered its money ask for Mitchell. Confirmed in code: rankSchedule (secretary.ts:386) sees only an active schedule and ensureRankSchedule (secretary.ts:183-201) returns the ended one, so no tool call restores it. Mitchell was told \"I rank once a day at 07:00\" in mt_mjxwzdhhd7 a day after the schedule ended, so the end was not meant."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-21T00:05:43.367Z"
sessionId: "se_a92b2s2jnn"
assignmentId: "as_89nclvr9pb"
costUsd: 1.3329805
tokens: 66649
turns: 29
createdAt: "2026-11-21T00:02:58.075Z"
updatedAt: "2026-11-21T00:05:43.367Z"
---
## What I did
I built on the journal line from 2026-11-20 ([dc_myj37sj0lp](2026-11-20-exploration-captains-can-t-decide-most-asks-in-the-j37sj0lp.md), gr_0vuiuqcw8p). That grant's step 2 stalled because captain request cr_0ncz8db1f3 got no card ([dc_cvh1v6emas](2026-11-20-live-check-with-a-second-captain-captain-request-s-h1v6emas.md)). I traced why, on the live town at 9ba1f937 and in the code. Findings are in [dc_n7ws2dhugo](../../note/2026-11/2026-11-21-exploration-2026-11-21-the-secretary-s-ranking-sch-ws2dhugo.md). I proposed gr_mcuj10tupi.

## Findings
- The Town Hall's "Daily ask ranking" schedule, sc_8zoclbtrwp, ended "past its end" at 2026-11-18T17:01Z. That was its 14-day default. It had run 12 times. The two weekly Town Hall schedules are active, but their retainer is "rejected", so they don't fire.
- secretary.ts `needsOverdue` and the decision run both need an active, funded ranking schedule. `ensureRankSchedule` never makes the schedule again once one exists, even if it has ended. So since 11-18 nothing renders Town Hall needs (captain and access requests), and the one-hour backstop for every building's needs is off too.
- cr_0ncz8db1f3 has been pending since 11-20 02:09Z. Its need en_kql3prs03u has no card: /api/asks lists 3 open asks and none of them is on it. Captain requests have no fallback view. The HUD lists only access requests for admins; captain requests show only in the goal tree panel.
- Proposal gr_mcuj10tupi "Captain and join requests always reach a human": M + S + S = 250k. Step 1: a retainer warns 3 days before it ends with a renewal need, and the ranking schedule is made again when it ended past its end. Step 2: a captain request with no card shows as a row in the decision queue with Accept and Decline. Step 3: a live check. Key results kr_oaf6jx34o8 and kr_m3bkqgnwd0. The town's estimate: 3 similar grants spent 178k–268k.
- Not verified: whether Mitchell meant the ranking schedule to end.

## What I need from you
Decide gr_mcuj10tupi in the decision queue. If the ranking schedule was meant to end, say so, and only step 2 ships.
