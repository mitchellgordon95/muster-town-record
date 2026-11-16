---
id: "dc_71g4u1zha3"
type: "report"
state: "building"
title: "Drag residents with a grasper hand: PR #477, parked on CI to merge"
authorId: "ag_1qzqco069n"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #477 (grasper-hand drag of residents, desk-drop rule, resolveFurniture swap fix) is parked on CI; its continuation as_hfosiuplt1 squash-merges on green. Mouse-only is fine for Mitchell's flag; touch long-press stays unbuilt unless he asks."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-16T18:33:36.015Z"
sessionId: "se_iomnvam5kf"
assignmentId: "as_usy2f2zqyg"
costUsd: 2.6076539999999997
tokens: 130383
turns: 46
createdAt: "2026-11-16T18:33:27.173Z"
updatedAt: "2026-11-16T18:33:36.015Z"
---
## What I did
I built Mitchell's flag [dc_mf6oelioq5](../../flag/2026-11/2026-11-16-ok-actually-let-me-just-click-and-drag-residents-t-6oelioq5.md) as one PR: https://github.com/mitchellgordon95/muster-town/pull/477 (draft). `npm run check --fast` passed: docs, knip, typecheck, and the affected tests (51 web files, 288 tests, plus core and server). The new tests are core `desk-drop.test.ts`, server `rest.test.ts` (desk-drop), and web `residentDrag.test.ts`. Topic page: [dc_kmrianpcp1](../../wiki/2026-11/2026-11-16-drag-residents-with-the-grasper-hand-rianpcp1.md).

## Findings
**To try it on live** (after merge and deploy): sign in as a human with building.manage on a building, or as admin. On the normal map, hover a resident or visitor: the cursor is a grab hand. Press and drag: a pixel fist holds the body, and a dashed outline marks the drop tile. A press without movement is still a click and opens the panel.

**The three drop cases** (`POST /api/agents/:id/desk-drop`, pure rule `core/world/desk-drop.ts`):
- **Another desk in the same room**, free or taken: the two desk *pieces* swap places, and the toast reads "A and B swapped desks".
- **Free floor in its room:** its desk piece moves so the agent stands on the drop tile, checked against the Edit layout rules. If a rule refuses, the toast reads "Can't put X's desk there: <rule>" and the body snaps back.
- **Anywhere else** (another building, grass, the Town Hall's fixed seats): the body snaps back with a one-line toast.

The bodies move at once. The furniture rebuild moves anyone sitting at the affected desks. The dragged agent goes to its new desk unless it is in a meeting or walking.

**Two places I differed from the brief:**
- The `desks` rows are never rewritten. A desk number is a fork's sandbox slot (`desk_slots`), so re-seating a running fork would switch its sandbox mid-session. "Take that desk" swaps the desk pieces instead.
- I found and fixed a bug in `resolveFurniture`. It accepted stored anchors one at a time, so a pure A↔B exchange was silently dropped on rebuild. It now accepts the whole stored set first when that set is legal.

Touch long-press is not built: drag works with a mouse only.

## What I need from you
Nothing needed. I'm parked on PR #477's CI and will merge it when it is green.
