---
id: "dc_yn8gl1rmyt"
type: "flag"
state: "building"
title: "can you take a UX pass on the goal tree editor? maybe move some stuff into a main modal? maybe a nice tree node display…"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "UX pass on the goal tree editor (Mitchell's flag dc_yn8gl1rmyt, verbatim: \"can you take a UX pass on the goal tree editor? maybe move some stuff into a main modal? maybe a nice tree node display? chat on the side? idk, take some screenshots and iterate please\").\n\nScope: the goal tree editor in the web client (Town Hall goal tree tabs / the tree view and its edit, propose, accept/cut controls; docs/goals.md and topic page \"Town-level goal tree (design)\" dc_0xqyrevla1 say what it does today; \"Web client panels and the in-tray\" dc_jcyf86dpdp covers the panel layout). Start by screenshotting the editor as it is now (skill \"demo-media\" dc_p68jzo79xq, topic page dc_32ndttkb57), write down the 3-5 worst UX problems you see, then iterate: build, screenshot, look, adjust. Mitchell's three ideas are suggestions, not a spec: a main modal for the editor instead of cramming it into the side panel, a proper tree node display (indent, expand/collapse, status, owner, dates, funded grant at a glance), and the 1:1 chat beside the tree so he can talk to the manager while editing. Use your judgment on which of these earn their place; drop any that don't and say why.\n\nShip it: PR to main, merge green, queue the redeploy, say which commit should be live; the live check can be a parked continuation on that deploy. Before/after crops ≤300 px tall in the report (at most 2 in the report, note which one is preferred for the rollup). The report must open with plain words on what Mitchell now sees when he opens the goal tree editor. Keep it to one PR if it fits; if the modal and the chat are each big, do the modal + tree node display first and queue the chat-on-the-side as a second assignment rather than leaving it half done."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T02:47:35.726Z"
flagPos: {"x":59,"y":2}
pickedUpAt: "2026-10-31T02:47:20.038Z"
pickedUpBy: "ag_mh0qidzgw6"
createdAt: "2026-10-31T02:47:08.874Z"
updatedAt: "2026-10-31T02:47:35.726Z"
---
can you take a UX pass on the goal tree editor? maybe move some stuff into a main modal? maybe a nice tree node display? chat on the side? idk, take some screenshots and iterate please
