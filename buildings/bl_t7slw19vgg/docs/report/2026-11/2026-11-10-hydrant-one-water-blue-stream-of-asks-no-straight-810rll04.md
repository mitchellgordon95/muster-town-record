---
id: "dc_47810rll04"
type: "report"
state: "building"
title: "Hydrant: one water-blue stream of asks, no straight jet (PR #414, parked on CI)"
authorId: "ag_175ajqy06p"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged: PR #414 (one water-blue stream of asks) parked on CI; as_594hhiyp58 already waits on {pr: 414} and merges if green. Nothing else queued."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-10T20:27:11.439Z"
sessionId: "se_1h76mvrprf"
assignmentId: "as_8m2ib0f65t"
costUsd: 0.5140726
tokens: 25704
turns: 9
createdAt: "2026-11-10T20:25:34.445Z"
updatedAt: "2026-11-10T20:27:11.439Z"
---
## What I did
Did the hydrant change Mitchell asked for in 1:1 mt_db6itzy2br and opened draft PR #414 (https://github.com/mitchellgordon95/muster-town/pull/414). The session is parked until its CI finishes.

## Findings
- **The straight blue stream is gone.** That was the notice stream, dots moving in an even line to the board. `streamParticles` (packages/web/src/map/hydrant.ts) now takes one target and draws one dot per open ask. Asks can now use all 12 dots (MAX_PARTICLES).
- **The arc is now blue instead of yellow.** It changed from #ffcf5e to **#7cc4ff**: the water blue the notice stream used, which is also the town's --accent colour. It still arcs and eases out to the Secretary's desk (renderer.ts drawStream).
- **Nothing else changed:** with reduced motion it still draws nothing. The counts still sync the same way, and noticesToday is still counted, just not drawn.
- **Checks:** typecheck passes and all 416 web tests pass. I rewrote the hydrant test for the single stream. docs/architecture.md and docs/legible-delegation.md §A now describe one stream.
- **Not checked yet:** I have not looked at the new colour on the live map. That needs the merge and a deploy.

## What I need from you
Nothing needed. When it resumes, this session will merge PR #414 if CI is green.
