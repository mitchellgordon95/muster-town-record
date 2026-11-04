---
id: "dc_hea8k2534l"
type: "report"
state: "building"
title: "PR #346 (Daily digest button) merged as dd99c595; parked on the deploy"
authorId: "ag_ytt3hlkewb"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_i50xwu4z2t","dc_jcs6svrnmt"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/346"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #346 (Daily digest button) merged as dd99c595, no redeploy. Parked on {deploy: dd99c595} (third and last park of the chain; prod is moving again, so it should resolve within the next promote). Live check (guest: no digestRun / no button; admin: button next to \"Talk to Secretary\") goes into rollup 47."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T19:55:37.864Z"
sessionId: "se_q3xdxxqtr2"
assignmentId: "as_elih8wm9vd"
costUsd: 0.2634338
tokens: 13172
turns: 5
createdAt: "2026-11-04T19:55:28.250Z"
updatedAt: "2026-11-04T19:55:37.864Z"
---
## What I did
PR #346's CI on 5206aba1 was green: check and image passed, and GitHub showed the PR as MERGEABLE/CLEAN. I merged it as **dd99c5957db29f13e3b264dca702f089b96d059d** and did not call redeploy, because CI's promote job deploys it. https://github.com/mitchellgordon95/muster-town/pull/346

## Findings
- The merge sha is dd99c595. It goes live when /api/health `commit` contains it.
- The live check for the next session is in two parts:
  - **Guest:** `GET /api/buildings/town-hall/intray` has no `digestRun` (it should be null), and the Town Hall in-tray header shows no "Daily digest" button.
  - **Signed-in admin:** the button sits next to "Talk to Secretary". It is enabled only once the retainer is approved and a rollup has arrived since the last card.
- This is the chain's third park, the last one allowed. If it drops, the live check has to come back as a fresh assignment.

## What I need from you
Nothing needed.
