---
id: "dc_xbhfursvgn"
type: "report"
state: "building"
title: "Meeting rooms now drawn as a table with chairs (draft PR #12)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T03:18:12.843Z"
sessionId: "se_dsyv9y7kov"
assignmentId: "as_n1kvq2x5t4"
createdAt: "2026-10-20T02:00:02.707Z"
updatedAt: "2026-10-20T03:18:12.843Z"
---
## Summary
I did what you asked about the meeting room not looking like one. It used to be a single row of 3–4 brown TABLE tiles, which looked like a counter. Now the table has a rim, an apron (the dark strip below the tabletop) and legs, with papers and mugs on it, and there's a chair on the free floor above and below each table tile. It's a web-only change: no server layout, places or walkability change. Draft PR: https://github.com/mitchellgordon95/agent-town/pull/12

## What I did
- `packages/web/src/map/sprites.ts`: redrew `drawTable` and added `drawChair(facing)`. The meeting panel icon now shows a chair behind the table.
- `packages/web/src/map/world.ts`: when the map is built, a second pass puts a chair on every FLOOR tile directly above or below a TABLE tile. It runs after the floor is drawn so the floor doesn't cover the chairs. The chair below sits on the existing stand tile, so an agent standing there looks seated.
- Added one line to docs/log.md.

## Findings / verification
- `npm run typecheck` passes. The web package has no tests.
- Preview: headless Chrome won't start in my sandbox because a library is missing (libnspr4), so I couldn't screenshot the live map. Instead I ran the real draw functions against a fake canvas that records the calls and drew the result with Python's PIL. It shows a 3-tile table with a paper and two mugs, three navy chairs above facing down and three seen from behind below. It clearly reads as a meeting table.
- Not verified: how it looks on the live map, especially the Town Hall's 4-tile table, where the row above should be floor.

## Proposal for next session
Can I get a real browser screenshot pipeline running at my desk (install the missing Chrome libraries, or a Playwright image)? Then every web PR could include an actual screenshot instead of a description. That's the main gap in how I verify visual changes.

## For others
- @Sage: I haven't checked the mock fixture for v1 role names yet. Next time I'm in `mock/`.
- @Root: noted that #9 makes terminal assignments throw (409). As far as I know, web code never reopens assignments.

## Questions for humans
- Could someone open PR #12 locally and look at the Town Hall table? I couldn't view the live map.
