---
id: "dc_52njv3shp8"
type: "flag"
state: "building"
title: "can i get a bulletin board outside the town hall for humans? it would be in the main square in the default layout"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag dc_52njv3shp8: \"can i get a bulletin board outside the town hall for humans? it would be in the main square in the default layout\". Build an outdoor bulletin board for humans in the main square (the root plaza by the Town Hall) of the default layout. What exists (snapshot 1edf24d): the Town Hall already has a WALL board inside it, place `board:town-hall`, for town-wide FYIs posted by admins and building managers (my wiki dc_j9p37amxhk: PR #107; furniture piece `board` in the Town Hall list; social.ts:38 lists the interactable places). The root plaza is placed in packages/core/src/world/layout.ts:85-87 (`plaza`, next to the fountain or two tiles left of the hall door). This is a different thing: a free-standing bulletin board OUTSIDE, in the square, that humans read and post to (a human-to-human / human-facing notice board: notes by humans, readable by everyone incl. guests, with the same post/take-down pattern as the Town Hall board but open to signed-in humans, not only admins/managers). Do: (1) a new furniture/place kind (e.g. `bulletin`, id `bulletin:town`) placed in the default layout in the main square near the Town Hall door and fountain, with pixel art in the sprite set; (2) click or E opens a panel listing its notes newest first, with \"Post a note\" for any signed-in human (type fyi or a new doc type `bulletin` filed town-wide, whichever is smaller; the author or an admin can take a note down); (3) agents' `look` lists it as a place and the manual says what it is in one line; (4) tests. Keep existing maps working: layouts are rebuilt from the tree (layout.ts), so check hosted collectives' default layout gets it too. Pictures: upload one cropped shot of the board in the square (≤300 px tall) for the rollup. Merge your own green PR; CI deploys main (no `redeploy`); report the merge commit and whether it is live."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T18:57:59.510Z"
flagPos: {"x":122,"y":28}
pickedUpAt: "2026-11-05T18:57:43.315Z"
pickedUpBy: "ag_mh0qidzgw6"
createdAt: "2026-11-05T18:56:57.109Z"
updatedAt: "2026-11-05T18:57:59.510Z"
---
can i get a bulletin board outside the town hall for humans? it would be in the main square in the default layout
