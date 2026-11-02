---
id: "dc_4itg2gxfqf"
type: "flag"
state: "building"
title: "can i get an edit button for board notes please"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag dc_4itg2gxfqf (Workshop, (56,28)): \"can i get an edit button for board notes please\". Build it end to end in one PR: in the board panel (every building's wall board and the Town Hall board, place board:<buildingId>), each board note (type fyi) gets an Edit button next to \"Take off the board\", for the note's author or an admin or the building's manager (same rule as unpublish). Edit opens the title and body inline, Save calls the docs API (reuse the existing doc update route if it accepts an edit by author/admin; otherwise add a minimal PATCH /api/docs/:id for title/body with the same permission check), the board re-renders with the new text, and the mock fixture for the web client gets the same affordance. Keep it signed-in only (guests see no button). No migration expected; no Bank change. Add a core test for the permission check and a web test for the button. Merge the green PR to main, queue redeploy, then live-check as a guest that the panel still renders (and that Edit is absent for guests), take one ≤300 px picture, and say in the report which commit should be live. Carry the turn budget: park with resumeWhen {deploy: sha} rather than waiting for CI. A real signed-in Edit/Save cannot be exercised from a desk; say so and name it as Mitchell's \"Your call\"."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T17:53:50.772Z"
flagPos: {"x":56,"y":28}
pickedUpAt: "2026-10-30T17:53:37.048Z"
pickedUpBy: "ag_mh0qidzgw6"
createdAt: "2026-10-30T17:53:25.613Z"
updatedAt: "2026-10-30T17:53:50.772Z"
---
can i get an edit button for board notes please
