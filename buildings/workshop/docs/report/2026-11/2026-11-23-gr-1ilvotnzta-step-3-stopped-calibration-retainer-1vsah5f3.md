---
id: "dc_191vsah5f3"
type: "report"
state: "building"
title: "gr_1ilvotnzta step 3 stopped: calibration retainer not funded yet, step 1 not live yet"
authorId: "ag_dxlo4haxz7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Taken in. The retainer decision already has its channel: ask ak_2uugrh04ob sits in the decision queue for Mitchell, so no second ask. Follow-ups queued: a deploy-wait check on 172c4ab4 that verifies kr_aus2bjpxxv, and a one-shot check on the schedule after the first calibration run (11-30 04:05Z) to claim kr_kdau1dt005 and bring the grant back for close."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-23T16:53:15.547Z"
sessionId: "se_r9h6p9dc25"
assignmentId: "as_0xr5m6pmyu"
costUsd: 0.4505534
tokens: 22528
turns: 12
createdAt: "2026-11-23T16:52:19.375Z"
updatedAt: "2026-11-23T16:53:15.547Z"
---
## What I did
I read the live town (16:51Z server time): /api/health, the Town Hall schedules and the open asks. I tried `calibrate` and ran the core calibration test. Then I rewrote topic page [dc_jjbqweg1qr](../../wiki/2026-11/2026-11-23-calibration-that-cuts-grant-holds-gr-1ilvotnzta-bqweg1qr.md). I stopped as the assignment says to when the retainer is still unfunded.

## Findings
- **The retainer is not funded.** sc_m9g7axmnoy "Weekly calibration" has retainer "asked", 80,000/run, and its next run is 2026-11-30T04:05Z. Its ask ak_2uugrh04ob is still open. The same holds for sc_wdiu7f3g4t (ask ak_22him8886f). Nobody has rejected them, so the grant's early-stop rule does not apply yet.
- **Step 1 is not live.** /api/health shows commit 6b32f5fe with deploy "behind" (prodTip e3fd8992, 4 commits behind). PR #577's commit 172c4ab4 is on main but is not an ancestor of either commit.
- **A fork cannot start a run.** `calibrate` returned "Only the Town Hall's Planner files a calibration ask." No calibration card exists in the queue.
- **Live measures** (/api/health legible): holdShare 26 held of 40 closed (0.65). spentOverSize is S 1.04 (n=29), M 0.84 (n=58), L 0.51 (n=3).
- **Proposal in code.** The core test planner-calibration.test.ts passes 9/9 on the 11-23 sample. Its proposal reads "Raise S from 50,000 to 120,000". It projects the hold share falling from 46% to 24%, against the line "23 of 37 grants closed in 14 days held before they closed (62%), over 25%". It never proposes 50,000 → 50,000.
- **Key results:**
  - kr_aus2bjpxxv can be claimed once 172c4ab4 is live. It is met in code and tests now.
  - kr_7otnsw3vf8 is already claimed.
  - kr_kdau1dt005 cannot be claimed. It needs the Planner's run, which needs ak_2uugrh04ob approved. The earliest scheduled run is 11-30 04:05Z, before its due date of 12-01.
  - The grant should not be closed yet. Either wait for the 11-30 run, with a short check session after it, or close it with kr_kdau1dt005 missed if the retainer is rejected.

## What I need from you
Decide whether to approve the weekly calibration retainer (ak_2uugrh04ob). Without it, no calibration card reaches the queue.
