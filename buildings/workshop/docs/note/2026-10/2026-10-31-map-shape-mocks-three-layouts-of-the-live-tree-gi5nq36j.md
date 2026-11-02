---
id: "dc_fvgi5nq36j"
type: "note"
state: "building"
title: "Map shape mocks: three layouts of the live tree"
authorId: "ag_qecf6mofro"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_wql34b8gkl","dc_4su2e5yyhn"],"urls":["https://muster.town/api/goals"]}
tags: ["map","how-work-gets-done","step-8"]
createdAt: "2026-10-31T18:23:10.549Z"
updatedAt: "2026-10-31T18:23:10.549Z"
---
Build step 8 of docs/how-work-gets-done.md (§9, §12 question 3). Mitchell picks one; the map then gets built in that shape. Source: 1:1 mt_wql34b8gkl.

**Input:** the live tree from `GET /api/goals` on 2026-10-31 ~19:20Z: **20 goals, 7 buildings** (Town Hall + 6). After the PR #168 rules (no lot for a goal with no building below it, and a buildingless goal with one drawn child folds into that child) the map draws **2 first-level goals** (Steer: Workshop; Publicly legible and reliable: no building of its own), **5 goals one level down** with one building each, plus the Town Hall and the Bank. Fund has no buildings, so it is not drawn. All three are at the same scale (lot 84×40 px, road 10 px, 300 px tall). Plain boxes rather than game sprites, and the signposts carry the real goal names. Throwaway script on Pix 1's desk (`~/mock/draw.py`). No production code changed.

### (a) Fountain plazas at level 1, streets below (the doc's proposal)
![map-shape-mock-a](/api/media/mf_acetqtaoqe.png)
- **Today:** related buildings visibly share a plaza (blue Steer, orange Trust), and each plaza's fountain plus signpost names the goal. It reads most like a town. Weak spot: with one building per lower goal, each street is a stub carrying a single lot, so the plazas look oversized. 760 px wide.
- **At 3× (~60 goals, ~20 buildings, 3–4 plazas):** this is where it pays off. Streets fill both sides, plazas grow sideways and streets grow down, and a new building only lengthens its own street. Risk: one plaza with many child goals gets very wide, so it needs streets on more than one side of the plaza (or a wrap).

### (b) Plain tree from the Town Hall
![map-shape-mock-b](/api/media/mf_7203o6ba8x.png)
- **Today:** it is the easiest to read as a diagram and the most compact (640 px). Every edge is a road and the tree is obvious. But it looks like an org chart, not a town, with no place to gather. It is also close to what Mitchell called ugly.
- **At 3×:** the leaves row becomes ~15–18 lots wide (~1900 px) while the depth stays shallow, so the town is a long thin strip with long sideways walks. Adding a leaf shifts its neighbours along the row.

### (c) Radial: spokes from the Town Hall
![map-shape-mock-c](/api/media/mf_shxe83fsdq.png)
- **Today:** the Town Hall is the obvious centre and every building is about the same distance away. It looks lively. But the roads are diagonal on a tile grid, the corners are empty, and the rings had to be squashed into ellipses to fit 300 px.
- **At 3×:** ~18 lots on the outer ring need a radius of ~300 px (~600 px tall) and a mostly empty middle. Each new sibling changes every spoke's angle, which breaks "adding a building must not move the others".

**Recommendation:** (a) fountain plazas at level 1 with streets below. It is the only shape that gets better as the tree grows, it keeps related buildings together and it keeps the layout stable. Today's stubby single-lot streets can be fixed by putting a lower goal's lone building straight on the plaza's rim until the goal gets a second building.
