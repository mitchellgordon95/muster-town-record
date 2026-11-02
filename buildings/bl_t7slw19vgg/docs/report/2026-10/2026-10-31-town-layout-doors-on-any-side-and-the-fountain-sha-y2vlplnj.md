---
id: "dc_ehy2vlplnj"
type: "report"
state: "building"
title: "Town layout: doors on any side and the fountain shape as a planned town (PR #205), parked on CI"
authorId: "ag_9otsjzyg2u"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked correctly; its continuation (as_i9vxfnelvj) merges #205 and redeploys once CI finishes."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-10-31T21:46:59.281Z"
sessionId: "se_bbtl8jqfuf"
assignmentId: "as_6gd7y6u4yz"
costUsd: 1.0615389999999998
tokens: 53077
turns: 35
createdAt: "2026-10-31T21:46:51.769Z"
updatedAt: "2026-10-31T21:46:59.281Z"
---
## What I did
- Picked up commit a0b44dc (doors on any side, square town) from the earlier session and merged origin/main into it; the only conflict was the docs/log.md line.
- Fixed the one knip dead export (`stepOut`).
- Iterated once more on full-map screenshots. The trees used to be a random forest; now a boulevard of street trees stands between the main street's lamps and the park scatter is sparser (30% down to 16%).
- Rewrote PR #205's body, which listed every commit in the repo, and marked it ready.

## Findings
- PR: https://github.com/mitchellgordon95/agent-town/pull/205 (head f46c8c1), mergeable, CI running. The typecheck passes, knip is clean, and core has 577/577 tests passing.
- Doors: a door can be in any wall (`Side` in core `world/road.ts`). In the fountain town, buildings stand back to back along each district's avenue with their doors facing it. Radial doors face the middle of the town. Tree-shape doors still face their street.
- The fountain shape is now its own planned town (`world/square.ts`). A paved square has a fountain, with the Town Hall on its north side and the Bank on its south side, both doors on the square. A main street runs east and west through it, lined with lamps and trees. Each first-level goal is a district on its own avenue, with parkland between districts.
- Pictures are on my desk at ~/maplab, a desk cache only:
  - before: before-fountain-map.png (one row of buildings under a sand strip with tiny fountains)
  - after: v4-map.png (the full planned town) and v4c-1280.png (the square at 1280×720)
  - phone: v3-sq-390.png
- The plan and the harness are on topic page [dc_004hyy29z6](../../wiki/2026-10/2026-10-31-town-layout-doors-on-any-side-the-planned-fountain-4hyy29z6.md).
- When agents are working, the guest's first view is the busiest building, not the square. That's existing "watch first" behaviour, so I didn't change it.

## What I need from you
Nothing needed. I resume when #205's CI finishes, then merge and redeploy.
