---
id: "dc_7zx9sglmkb"
type: "report"
state: "building"
title: "Hydrant moves to the outbox's spot, outbox off the map: PR #457, parked on CI"
authorId: "ag_r8ojaz4urt"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. PR #457 does flag dc_f3xcob2n9u (hydrant to (2,6), outbox counter/place/badge/icon/help line removed, PanelKind kept). The merge-on-green continuation is already parked as as_7p0rr9o4jw waiting on PR 457; nothing else to queue."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-15T21:06:19.067Z"
sessionId: "se_on7ov7iti9"
assignmentId: "as_5bfawuib48"
costUsd: 1.4244550000000002
tokens: 71223
turns: 31
createdAt: "2026-11-15T21:06:00.092Z"
updatedAt: "2026-11-15T21:06:19.068Z"
---
## What I did
Did Mitchell's flag [dc_f3xcob2n9u](../../flag/2026-11/2026-11-15-move-the-fire-hydrant-from-the-corner-to-where-the-xcob2n9u.md) in one PR: https://github.com/mitchellgordon95/muster-town/pull/457. `npm run check` is green locally: docs, deadcode, typecheck and all tests, 7 min.

## Findings
- **Hydrant moved.** It went from the corner (15, 9) to the left tile of the old outbox counter (2, 6), in Town Hall coordinates. People use it from the tile below, (2, 7), and the Secretary still rests beside it. The town-hall-rests tests pass, and the stream code needed no change. The corner (15, 9) and the counter's right tile (3, 6) are now open floor. The live Town Hall has no stored furniture override (`furniture: {}` from /api/buildings/town-hall), so the new default is what goes live.
- **Removed from the map:** the outbox counter piece, the `outbox` place (core and mock), the badge on the map, the `outbox` icon and the help-card "Requests counter" line. I also removed the web's dead `state.outbox` / `outboxRev` plumbing and its test.
- **Kept on purpose:** the `outbox` PanelKind, so an old outbox link still opens the decision queue. The server's snapshot count and the request API are unchanged.
- **Docs and tests:** docs/architecture.md is updated, and the log entry is in docs/log.d/2026-11-15-teo-1-hydrant-to-outbox-spot.md. The furniture, layout, hydrant and helpCard tests are updated.
- **What a human will see once it is live:** the hydrant on the left side of the Town Hall, just left of the user stats stand, and no outbox counter. The bottom-right corner is empty floor.

## What I need from you
Nothing needed. The next session squash-merges PR #457 when its CI is green.
