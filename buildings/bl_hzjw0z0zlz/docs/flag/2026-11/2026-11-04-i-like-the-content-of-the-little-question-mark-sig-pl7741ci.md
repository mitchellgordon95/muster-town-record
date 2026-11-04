---
id: "dc_qppl7741ci"
type: "flag"
state: "building"
title: "i like the content of the little question mark signs in each building. but let's make it even cooler. i'm thinking like…"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag (dc_qppl7741ci, verbatim): \"i like the content of the little question mark signs in each building. but let's make it even cooler. i'm thinking like the building gets highlighted and the rest kind of gets a shadow, and then you can click / hover on different parts of the building and see what they do. idk, i'm not saying it precisely but i think you can envision the UX i'm thinking of.\"\n\nBuild it: turn the building \"?\" help sign into a guided look at the building on the map itself.\n\nWhat to ship (one PR, Onboarding's code: packages/web/src/panels/HelpSign.tsx, helpCard.ts, hiw.css, and the map renderer packages/web/src/map/renderer.ts where it draws the overlay/hit areas):\n1. Opening a help sign (place help:<buildingId>) puts the map in a \"tour\" of that building: the camera centres on the building, everything outside the building's footprint gets a translucent dark shadow, the building stays lit (a soft outline/glow around its footprint). The paper card no longer covers the map: shrink it to a slim side sheet (or a bottom strip on narrow screens) that keeps the title, \"Working on\", manager/working-now and \"What you can do\" + sign-in buttons; the \"What's here\" list stays but becomes the legend for the hotspots.\n2. Every thing in the building that helpCard.things lists (in-tray, board, cabinet, meeting room, schedule board, desks, door…) is a hotspot on the map: hover shows a small paper tooltip with that thing's name and its helpCard line (same copy source, no new copy); click walks there and opens it, as the list rows do today (store.walkTo + placePanel). Hovering a hotspot also highlights the matching row in the legend and vice versa.\n3. Touch (pointer: coarse): a tap on a hotspot shows the tooltip with a \"Go\" button; a second tap or \"Go\" walks. Keyboard: Tab moves through the legend rows, Esc leaves the tour.\n4. Leaving: Esc, the × on the sheet, clicking the shadowed area, or walking to a thing ends the tour and removes the shadow. The tour must never leave the map dimmed after the card is gone.\n5. Keep the current HelpSignCard content and viewer logic (guest/pending/member/reviewer) intact; only its layout and the map treatment change. Follow the muster-style-guide skill (dc_q736158pnn) for the paper look; read topic page dc_axuboivkud first for how the sign and its copy work now.\n\nRules: ship it directly (no setting or flag), green PR, merge your own PR, `redeploy`, say which commit should be live in your report, and park with resumeWhen {deploy: sha} to check it live on muster.town (desktop + 390px) before you call it done. Extend packages/web/test/helpCard.test.ts if the copy model changes. Budget: aim under 400k tokens; if the renderer work is bigger than that, ship the shadow + lit building + hotspots with tooltips first and report what is left."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-04T17:42:05.192Z"
flagPos: {"x":74,"y":12}
pickedUpAt: "2026-11-04T17:41:30.481Z"
pickedUpBy: "ag_s1n1xknj8n"
createdAt: "2026-11-04T17:41:16.021Z"
updatedAt: "2026-11-04T17:42:05.192Z"
---
i like the content of the little question mark signs in each building. but let's make it even cooler. i'm thinking like the building gets highlighted and the rest kind of gets a shadow, and then you can click / hover on different parts of the building and see what they do. idk, i'm not saying it precisely but i think you can envision the UX i'm thinking of
