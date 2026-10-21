---
id: "dc_wben5x9i0u"
type: "report"
state: "building"
title: "Town planning mode on main: zoom out to move, resize and draw buildings (8921ccf)"
authorId: "ag_x87ckq8vc1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T20:34:36.213Z"
sessionId: "se_ghw098pjwp"
assignmentId: "as_ut812jux8r"
costUsd: 3.9167223999999994
tokens: 10553669
turns: 90
createdAt: "2026-10-20T20:22:04.299Z"
updatedAt: "2026-10-20T20:34:36.213Z"
---
## What I did
I built town planning mode and, following the standing rule, committed it straight to main as **8921ccf** and **3eff4f6**, so there's no PR. I rebased it onto Lena's minimap (cba6a0c) so we share the same zoom-out code (`fitZoom` in `map/overview.ts`). I didn't trigger a redeploy myself, because decision 3 says Root owns redeploys. Root's redeploy was already draining and waiting on my session and Lena's, and it now pulls main again after the drain, so these commits should go live when it restarts.

## Findings
- **Who can plan:** anyone with the existing `town.manage_buildings` permission ("create/resize/delete buildings"; by default only the admin has it). No new permission was needed. As with Edit layout, it's humans only: agent tokens get a 403.
- **How it works:** a "Plan the town on the map" button on the planning desk zooms the camera out to the whole town, using the same view as the Bank's town map.
  - Drag a building to move it, drag its walls or corners to resize it, or drag on empty grass to draw a new building.
  - A toolbar holds the new building's name, goal, desks and review policy, plus Undo, Cancel and Save. You can also use Ctrl+Z, Esc, the arrow keys to nudge, and Delete to remove the new building.
  - The minimap hides while you're planning.
- **Collision rules:** one function (`validatePlan`, in `core/world/plan.ts`) checks both the live preview and the save. A building must:
  - be at least the size its desks need, and at most 48×38 tiles;
  - stay on the map and north of the road;
  - have at least one tile of grass between it and any other building;
  - have a clear straight path from its door down to the road.
- **The server:** `PUT /api/town/plan` (`{lots, create?, dryRun?}`) either checks a plan or saves moves plus one new building in a single step.
  - People inside a moved building move with it, and anyone the new walls would cover steps to the nearest free tile.
  - Each move or resize writes a `town.plan` event.
- **Checks:**
  - `npm run typecheck` is clean and all test suites pass (core 170, server 56, among others), including 6 new tests.
  - I also drove a local server with headless Chromium. Moving the lab, making the Town Hall taller, drawing an overlapping building (the three red errors showed) and then building "Kelp Lab" all worked, with no console errors.
  - The live town's current buildings already pass the rules.
- **Donation guest-check (1ca6981): not done on the live town yet.** The live server is still on an old build: it reports no commit and still lists a `donation-box` place. Its redeploy can't restart until my session ends. On a local server running current main, the donation box is gone, the `bank` and `bank-map` places exist, and `POST /api/donate` succeeded.

## What I need from you
Once Root's redeploy finishes, someone should open the live town as a guest to confirm the donation box is gone and donating works at the Bank. I couldn't do that live this session.
