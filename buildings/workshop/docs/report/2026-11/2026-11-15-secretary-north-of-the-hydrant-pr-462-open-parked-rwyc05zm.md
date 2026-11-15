---
id: "dc_qrrwyc05zm"
type: "report"
state: "building"
title: "Secretary north of the hydrant: PR #462 open, parked on CI"
authorId: "ag_jiym9o4n9h"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-15T22:11:04.941Z"
sessionId: "se_wkan7bam5j"
assignmentId: "as_yfukaigu3u"
costUsd: 0.9471983
tokens: 47360
turns: 24
createdAt: "2026-11-15T22:11:04.929Z"
updatedAt: "2026-11-15T22:11:04.941Z"
---
## What I did
Fixed Mitchell's flag [dc_zkzi4xnue4](../../flag/2026-11/2026-11-15-nit-move-the-secretary-north-of-the-fire-hydrant-h-zi4xnue4.md) and opened PR https://github.com/mitchellgordon95/muster-town/pull/462. `npm run check --fast` passed locally, with typecheck, knip and the affected tests all green (the tests took 7m53s). The work is now parked until CI finishes.

## Findings
- **Change:** a furniture `Piece` can now name its own `rest` tile, measured in map north, so it does not flip for a north-door room. The hydrant's rest tile is the one just above it, (2, 5) in the hall. `restBy` in layout.ts tries that tile first. If it is taken, unwalkable or a stand, it falls back to the old right/left/below/above search beside the stand. The Planner's spot is unchanged.
- **Test:** packages/core/test/town-hall-rests.test.ts now checks that the Secretary's desk is exactly the tile north of the hydrant cell. The existing checks still pass: the spot is walkable, inside the Town Hall, and on no other place's tile.
- **Stream dots:** the code in renderer.ts did not change. The dots still start at the top of the hydrant and settle at the Secretary's desk, which is now just above it. They should look like a short spurt up into his feet, but I have not seen this yet.
- **Docs:** I updated docs/architecture.md and added the log entry docs/log.d/2026-11-15-pix-1-secretary-north-of-hydrant.md.
- **Next session:** if CI is green, mark #462 ready and merge it (no redeploy). Once /api/health shows the merge sha, look at the live Town Hall map: the Secretary should stand at (2, 5) with the hydrant visible below him. Take a screenshot if possible.

## What I need from you
Nothing needed.
