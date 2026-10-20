---
id: "dc_ba81zl5d2u"
type: "report"
state: "building"
title: "Filing cabinet is now furniture you walk up to; PR #24 merged"
authorId: "ag_x87ckq8vc1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T04:08:01.451Z"
sessionId: "se_hjinqzeapg"
assignmentId: "as_0x100nuqb3"
costUsd: 0
tokens: 0
turns: 0
createdAt: "2026-10-20T03:56:55.449Z"
updatedAt: "2026-10-20T04:08:01.451Z"
---
## What I did
Turned the filing cabinet into a piece of furniture on the map in each lab, added it to PR #24, brought the branch up to date with main twice, and merged it as you asked: https://github.com/mitchellgordon95/agent-town/pull/24 (merge commit 1d3a037).

## Findings
- **The cabinet is on the map.** Each lab now has a place called `cabinet:<buildingId>`: a grey steel filing cabinet with its top drawer open and folders showing. It stands against the top wall, two tiles right of the board. Walk up and press E to open its panel ("Open the … filing cabinet"). The panel lists the building's reports and meeting notes, newest first.
- **The board panel lost its "Filing cabinet" tab.** The board's subtitle now says the reports and notes are in the cabinet beside it. The building overview has a new "Walk to the filing cabinet" link. Agents see the cabinet in `look`, just as they see the board.
- **Files changed:** the schema (new `TILE.CABINET = 15` and a new `cabinet` place type), the core and mock layouts, the sprite, the map drawing code, the code that picks the panel for each place, the app, the board and building panels, the README, architecture.md and the log.
- **Merge conflicts:** main changed twice while I worked (#19–#23, then #25–#26). Both times only `docs/architecture.md` and `docs/log.md` conflicted. I kept both sides each time; no code conflicted.
- **Checks:** `npm run typecheck` is clean. `npm test` passes all 165 tests. The core layout test now also checks that the cabinet tile is on the top wall and can be reached from the lab door and from the plaza.
- **Not checked in a browser.** Headless Chromium on my desk is missing system libraries (libnspr4 and others), and I can't install them without root. My desk container predates the #19 image change. So nobody has seen the cabinet drawn on screen yet. Have a quick look on the live map.
- I merged into main through the PR because you told me to directly. I did not push to main.

## What I need from you
Glance at a lab on the live map to confirm the cabinet looks right; I couldn't render it.
