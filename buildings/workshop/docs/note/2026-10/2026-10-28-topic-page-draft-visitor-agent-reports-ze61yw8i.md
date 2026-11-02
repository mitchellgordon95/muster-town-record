---
id: "dc_dnze61yw8i"
type: "note"
state: "building"
title: "Topic page draft: Visitor agent reports"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["topic-page-draft"]
createdAt: "2026-10-28T19:24:17.720Z"
updatedAt: "2026-10-28T19:24:17.720Z"
---
State on 2026-10-28. Background article "Visitor agents today" [dc_04i3sll7q5](../../article/2026-10/2026-10-27-visitor-agents-today-i3sll7q5.md). Join KR kr_4li00ad46e (starter brief on a visitor's first look) has no funded grant; the visitor-shape choice A/B/C (gr_f5bmciloqy, Pix recommends B) is Mitchell's TODO: don't ask again.
- Live since bdbc56e: an unhomed visitor (on the bench, the plaza, or in someone's lab) files submit_report under town-hall, tagged "visitor", with an owner footer in the body. Homed visitors file in their building as before.
- domain.ts isTownHallItem treats visitor-tagged town-hall reports as Town Hall items (intrayOf); GET /api/buildings/town-hall/intray → {reports, grants, access, blocked}. Web IntrayRow shows a "visitor report" pill; mock doc dc_visitor_r1.
- POST /api/agents/visitors is 403 for users without interact (app.ts write gate plus a route check in server routes/agents.ts).
- Not verified live end to end: no visitor has filed a report yet, and desks have only a resident token (MUSTER_TOWN_TOKEN), so an agent can't play a visitor.
- Code: verbs/docs.ts submit_report. Tests: core test/visitors.test.ts "visitor reports reach a human"; server test/access.test.ts.
