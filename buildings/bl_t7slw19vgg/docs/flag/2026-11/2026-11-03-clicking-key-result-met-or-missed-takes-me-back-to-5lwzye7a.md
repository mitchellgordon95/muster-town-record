---
id: "dc_nm5lwzye7a"
type: "flag"
state: "building"
title: "clicking \"key result met\" or missed takes me back to the intray overview. that's annoying when there's multiple buttons…"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag: clicking \"key result met\" or \"missed\" on a grant in the Town Hall in-tray sends him back to the in-tray overview; with several key results to mark he has to reopen the grant each time. Make it stay on the grant: after a key-result mark, reload the data and re-render the same focused grant (showing the new status on that key result's line). Leave the grant only when nothing is left to decide on it, and even then keep the view (with its updated state) rather than jumping away unless every decision on it is done. Likely cause: packages/web/src/panels/Places.tsx:82, where focusRow's onDecided does setFocus(null) + list.reload(); the mark buttons are at Places.tsx:581 (mark(k.id, ...)). Also check the same thing in the review deck (ReviewDeckView, line 95: it should not skip to the next slide on a single key-result mark) and in DocView's onDecided (line 88) if a rollup carries the key-result buttons. Fix only the key-result marks; whole-grant decisions (fund/counter/reject/continue/cut) may still return to the overview. Open a PR, merge when green, redeploy, and say in the report which commit should be live."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-03T22:58:58.285Z"
flagPos: {"x":82,"y":12}
pickedUpAt: "2026-11-03T22:58:47.446Z"
pickedUpBy: "ag_s1kuuuo54b"
createdAt: "2026-11-03T22:58:37.034Z"
updatedAt: "2026-11-03T22:58:58.285Z"
---
clicking "key result met" or missed takes me back to the intray overview. that's annoying when there's multiple buttons on the report to click, it should just stay on the report
