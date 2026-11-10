---
id: "dc_7x3ifhgmtw"
type: "report"
state: "building"
title: "PR #404 live: prose-read asks now read as whole sentences on /api/asks"
authorId: "ag_xjljtk6ajs"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR #404 live at 105456dd, five clipped ask titles repaired by the boot repair, all 27 open asks read whole. The mis-typed money asks you found (ak_964oxnm14w, ak_4nc6kwr1wt) go on the queue as their own exploration fix."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-09T23:34:44.781Z"
sessionId: "se_nx71s54itf"
assignmentId: "as_3fw42z2jb6"
costUsd: 0.3081298
tokens: 15406
turns: 6
createdAt: "2026-11-09T23:34:17.370Z"
updatedAt: "2026-11-09T23:34:44.781Z"
---
## What I did
Checked that /api/health has commit 105456dd (PR #404), so it is live. Read every open ask on GET /api/asks. Rewrote topic page [dc_rdx7am7r9q](../../wiki/2026-11/2026-11-09-grant-titles-and-how-asks-name-a-grant-x7am7r9q.md).

## Findings
- The boot repair `retitleProseAsks` ran at 23:33:42Z. It added a `retitled` history entry to five asks: ak_n60qsw0bac, ak_rjm3roy9v9, ak_v9sotn1myp, ak_964oxnm14w and ak_emigaxsalm.
- These titles now read as whole sentences:
  - "A 1" is now "A 1:1 with Juno when you have time, as you said in your 1:1 with Secretary".
  - "Optional" is now "Optional: give the test account dungeonrpg99-ops "direct work under" the Onboarding goal so a fork can check the stranger's 1:1 path".
  - The repo ask is now "Create one empty repo under dungeonrpg99-ops and give MUSTER_TEST_GH_TOKEN Contents read/write on it".
  - "Continue" is now "Continue, adjust or cut the three held Workshop grants from their cards in your in-tray".
  - ak_emigaxsalm no longer ends mid-phrase on "so".
- Every one of the 27 open asks has a title of 4 words or more. None ends mid-phrase.
- I noticed one problem and did not fix it. Two asks are filed as money asks against a grant, but they are not money asks: ak_964oxnm14w (the repo ask) and ak_4nc6kwr1wt. The rollup prose was read as a money ask on a grant. A future proposal could fix this.

## What I need from you
Nothing needed.
