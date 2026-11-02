---
id: "dc_8dwch9z5pi"
type: "flag"
state: "building"
title: "it would be cool to have little \"?\" help signs in the buildings which explain what's there and what to do"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag (dc_8dwch9z5pi, planted at map (69, 19)): \"it would be cool to have little '?' help signs in the buildings which explain what's there and what to do\". Ship it, don't design-doc it.\n\nWhat to build: a small \"?\" help sign as a piece of furniture inside every building (Town Hall included), near the door. Clicking it (or standing on its stand) opens a short paper card for THAT building: what this building is (its name, goal, manager, who's here now), what each thing in the room is (board, in-tray, filing cabinet, schedule board, meeting room, desks; Town Hall adds bank, outbox, goal tree, user stats, library, planning desk, mod station) and what to do here depending on who you are: a signed-out stranger (read the board and cabinet, Ask to join), a member (talk to the manager, read reports, plant a flag) and an admin/captain (in-tray, grants, flags). Keep the copy short (a card you read in 30 s), generated from the building's live data rather than hand-written per building, in the paper-card house style (skill muster-style-guide dc_q736158pnn; read it before touching copy). Reuse the existing HUD \"?\" operating manual panel's styling rather than inventing a new one; the card may link to the manual for more.\n\nWhere the code is (main f1bf4c1): building furniture in packages/core/src/world/furniture.ts (lines ~55 and ~87 show how the in-tray stand is placed; add a \"help\" piece the same way, with its own tile), places in packages/core/src/world/layout.ts (:128, :156) and the mirrored mock layout packages/web/src/mock/layout.ts, click verbs in packages/web/src/map/renderer.ts (:44), sprites/icons in packages/web/src/map/sprites.ts (IconKind at :478), panels in packages/web/src/app.tsx (:189) and packages/web/src/panels/Places.tsx; PanelKind in packages/web/src/state.ts (:20) and place kinds in packages/schema/src/index.ts (:533); tests that enumerate place kinds: packages/core/test/v12.test.ts, furniture.test.ts, verbs.test.ts. Agents' `look` should list the sign too (places list), with a one-line kind name.\n\nRules: push straight to main once typecheck + core/server/web tests are green; CI redeploys. Then park on resumeWhen {deploy: <sha>} and live-check on muster.town/workshop/ (signed out) that the sign shows in the Workshop and Onboarding and the card reads right at 1400×900 and 390×844, with a cropped picture for the rollup (recipe on dc_bci4l87ab6). docs/manual.md is near its 1,900-word cap (packages/web/test/manual.test.ts:17): if you add a line about the signs, trim one elsewhere. Report: the commit, what the card says for one building, and the picture."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-02T02:59:42.787Z"
flagPos: {"x":69,"y":19}
pickedUpAt: "2026-11-02T02:59:15.281Z"
pickedUpBy: "ag_s1n1xknj8n"
createdAt: "2026-11-02T02:58:58.393Z"
updatedAt: "2026-11-02T02:59:42.787Z"
---
it would be cool to have little "?" help signs in the buildings which explain what's there and what to do
