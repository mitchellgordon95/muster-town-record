---
id: "dc_pkqhs54k2q"
type: "report"
state: "building"
title: "Key-result marks keep you on the grant: works (checked in the mock town, live is 80da4cb)"
authorId: "ag_6balq761iz"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Verified in the mock town at 1280×720: a mark keeps the grant open in the in-tray and keeps the deck on the same slide. Live is 80da4cb. PR #288 (mock-only deck fix) queued for merge separately."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-03T23:33:35.362Z"
sessionId: "se_bp33lfocho"
assignmentId: "as_n4c7st2b0w"
costUsd: 1.0293291000000002
tokens: 51466
turns: 31
createdAt: "2026-11-03T23:33:23.783Z"
updatedAt: "2026-11-03T23:33:35.362Z"
---
## What I did
Confirmed live is on 80da4cb (`/api/health` at 2026-11-03 23:28 UTC). I did the check in the **mock town (VITE_MOCK=1), not on live**. The only live grant with claimed key results is the delight checkpoint gr_ukrou4zjha, and marking those is Mitchell's call. I used a Playwright script at 1280×720 on the mock grant gr_stress, which has 2 claimed key results.

## Findings
- **In-tray:** I opened gr_stress from the Town Hall in-tray and marked key result 1 met. The grant stayed open, with "← In-tray" still showing. Key result 1 now reads "· met" and key result 2 still reads "· claimed" with its Mark buttons. Marking key result 2 closed the grant view, and the grant left the in-tray (0 matches in the list).
- **Review deck:** On the gr_stress slide (7 / 7), marking key result 1 met kept the deck on slide 7 / 7, on the same grant: key result 1 "met", key result 2 "claimed". gr_stress is the last slide, so the counter staying the same proves little by itself. What shows the deck stayed put is that the same grant's key-result lines are still there, now with the new status.
- **Screenshot** (grant still open after one mark, 300 px tall): ![grant stays open after a mark](/api/media/mf_stxbep2e4j.png)
- **Side fix:** the mock review deck showed only slide 1. It asked for the in-tray of `"town-hall"`, but the mock Town Hall's id is `bl_townhall`. I fixed that one line in draft PR https://github.com/mitchellgordon95/muster-town/pull/288 (mock only; typecheck green, web tests 286/286). Live code is unchanged.
- No page errors.

## What I need from you
Nothing needed.
