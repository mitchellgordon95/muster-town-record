---
id: "dc_hsdvn0h5ho"
type: "flag"
state: "building"
title: "not anyone who logs in with github should be able to interact with the town. i think we need like a permissions system?…"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag dc_hsdvn0h5ho: \"not anyone who logs in with github should be able to interact with the town. i think we need like a permissions system? so people can ask for access and i can grant them roles in the collective?\" Build the smallest permissions system that answers this, in two halves, both yours.\n\nHalf 1 (first, under 600 k tokens): a design note filed in the building (type note) that states what is true today and the minimal design. Read first: Craig's PR 3 eac2e24 (visitor GitHub OAuth sign-in, mock GitHub; packages/server auth/session code), the admin token (data/admin-token, how the server checks it), the existing user/role fields in packages/schema/src/index.ts, and the guest card / How-this-works overlay copy (skill muster-style-guide dc_q736158pnn) so the wording of \"request access\" fits the house style. The design: (a) roles per collective, at least visitor (signed in with GitHub, read-only: same as a guest but named), member (can move, talk, use desks/benches/planning desk, whatever \"interact\" means today), admin (Mitchell: grants roles); (b) a signed-in visitor sees a \"Request access\" action on the guest card with an optional one-line message, and the request lands where Mitchell already looks (Town Hall in-tray or the mod station: pick the one that fits the code, say why); (c) the admin grants or declines from that place, and the person sees the result on their next load; (d) every write endpoint checks the role, not just \"logged in\"; (e) a visitor who was never granted anything can still read everything a guest can. List the endpoints that change and which existing tests cover them. Keep it to one page; no new infrastructure (no email, no external services).\n\nHalf 2 (same assignment, after the note is filed): implement that minimal design on main (push directly, house rule), with tests for the role check on at least one write endpoint and for the request → grant round trip, typecheck and server tests passing, the UI checked at 1400×900 and 390×844 with VITE_MOCK=1 as the style guide says. Then queue nothing: say in your report which commit should go live and that a redeploy is needed (you lack the redeploy permission; I will queue it). If half 2 does not fit in the session, file the note, push what passes, and report with verdict continue and a precise next step.\n\nReport: what is true today (with file:line), the design in five lines, what you shipped (commit), what is left, and under \"What I need from you\" the one thing Mitchell must decide (for example, whether he is the only admin or whether members can invite)."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-26T21:05:06.565Z"
createdAt: "2026-10-26T20:36:03.911Z"
updatedAt: "2026-10-26T21:05:06.565Z"
---
not anyone who logs in with github should be able to interact with the town. i think we need like a permissions system? so people can ask for access and i can grant them roles in the collective?
