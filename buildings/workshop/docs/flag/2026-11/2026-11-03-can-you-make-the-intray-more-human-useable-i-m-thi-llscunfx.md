---
id: "dc_2hllscunfx"
type: "flag"
state: "building"
title: "can you make the intray more human useable? i'm thinking of at least a view that has each report subject on one line th…"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag dc_2hllscunfx (verbatim): \"can you make the intray more human useable? i'm thinking of at least a view that has each report subject on one line that you can click into, instead of basically the whole report on the first page of the inbox\".\n\nBuild a compact list view of the in-tray and make it the default for humans. What is there today (packages/web/src/panels/Places.tsx): IntrayPanel (:37) renders, for the Town Hall, TownHallIntray (:166) whose \"Manager reports\" section uses IntrayRow (:657) for every report, and IntrayRow puts the rollup's Shipped cards inline (`intray-cards`, RollupCards, :694), the \"Needs:\" line (:686), the flag preview (:688), the chain line (:695) and the \"covers N reports\" expander (:704) all on the list page; GrantRow / RetainerRow / CaptainRow rows for proposals, checkpoints, retainers are tall too. Every building's own in-tray (:91-94) uses the same IntrayRow.\n\nWhat to ship (one PR, no feature flag, town FYI dc_0tbo60bn6l):\n1. A compact mode: one line per item in every section (manager reports, proposals, checkpoints, retainers, captains, join requests, goal proposals, closed-as-done, stopped): a small building tag / author portrait, the title (truncated with an ellipsis, full title in the tooltip), and at the right a time-ago plus at most one short status pill (rollup / flag / verdict, or the grant's status and spent/granted). No inline cards, no Needs line, no chain line, no covered list, no decision buttons on the line. Clicking the line opens the item (DocView with review for reports, the grant / retainer / request detail with its decision buttons, as the row does today).\n2. A toggle in the in-tray head next to \"Review as deck\" (Compact / Cards, or List / Expanded; pick clear words), remembered in localStorage; compact is the default for a signed-in human, the current expanded rows stay as the other mode so nothing is lost. Apply it to both the Town Hall in-tray and the buildings' in-trays (same IntrayPanel).\n3. Keep the pending count, the Mine / All / Funded-by-me filter and the sections' order; the sections stay as headings so the list reads like an inbox grouped by what kind of decision it is.\n4. A web test for the compact row (one line per item, title + pill, click opens) next to the existing in-tray tests (packages/web/test/rollupCards.test.tsx, reviewDeck.test.tsx).\nThen merge if green, redeploy, and after it is live take one cropped picture (≤300 px tall) of the Town Hall in-tray in compact mode with real items, uploaded as an mf_ id, and put it in your report with the live commit. If the in-tray is empty at that moment, use the Workshop in-tray or a mock dev server as Pix 1 did for mf_iu22vr4eu2 and say so."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-03T22:32:37.910Z"
flagPos: {"x":75,"y":12}
pickedUpAt: "2026-11-03T22:32:00.985Z"
pickedUpBy: "ag_mh0qidzgw6"
createdAt: "2026-11-03T22:31:47.599Z"
updatedAt: "2026-11-03T22:32:37.910Z"
---
can you make the intray more human useable? i'm thinking of at least a view that has each report subject on one line that you can click into, instead of basically the whole report on the first page of the inbox
