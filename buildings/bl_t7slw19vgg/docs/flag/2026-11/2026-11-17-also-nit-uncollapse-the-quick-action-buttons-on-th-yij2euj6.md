---
id: "dc_7jyij2euj6"
type: "flag"
state: "building"
title: "also nit: uncollapse the quick action buttons on the building's overview page. we've taken progressive disclosure a tou…"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag dc_7jyij2euj6 (planted at (42,6) in the UI / UX just now): \"also nit: uncollapse the quick action buttons on the building's overview page. we've taken progressive disclosure a touch too far.\"\n\nWhat he means: in packages/web/src/panels/BuildingPanel.tsx lines 105-129 the walk-to buttons (board, filing cabinet, manager's desk, hydrant, meeting table, goal tree, Edit layout) are folded under a `<details className=\"walk-fold\">` whose `<summary>` reads \"Go to: board · filing cabinet · …\". That fold came from gr_zak30564zh step 4 (\"the first screen keeps the summary\"). Undo it: render the `.walk-links` buttons directly on the Overview tab, always visible, no `<details>`/`<summary>`, and drop the module-level `walkOpen` state if nothing else uses it. Keep the \"N waiting\" warn pill next to the manager's-desk / hydrant buttons (it already is inside the buttons). Check the CSS for `.walk-fold` (packages/web/src/styles or wherever it lives) and remove dead rules; make sure the buttons lay out compactly (a wrapped row or tight grid, not one tall column) so the Overview still fits a laptop screen and the phone sheet. Do not touch the \"Talk to ★ manager\" / \"Plant a flag\" actions row or the schedule `.kr-more` fold, which Mitchell did not mention. Run the web typecheck and existing BuildingPanel tests, update any test that asserts the summary line, add a docs/log.d entry, open a PR, mark it ready and squash-merge when green (no redeploy). In your report say which commit should be live and what Mitchell will see on a building's Overview tab."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-17T03:55:53.666Z"
flagPos: {"x":42,"y":6}
pickedUpAt: "2026-11-17T03:55:07.912Z"
pickedUpBy: "ag_s1kuuuo54b"
createdAt: "2026-11-17T03:54:56.011Z"
updatedAt: "2026-11-17T03:55:53.666Z"
---
also nit: uncollapse the quick action buttons on the building's overview page. we've taken progressive disclosure a touch too far
