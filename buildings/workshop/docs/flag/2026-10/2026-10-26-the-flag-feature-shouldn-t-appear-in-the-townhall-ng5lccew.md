---
id: "dc_7qng5lccew"
type: "flag"
state: "building"
title: "the flag feature shouldn't appear in the townhall intray. it should just be a button binding, along with wasd, tab, E, …"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag (dc_7qng5lccew): \"the flag feature shouldn't appear in the townhall intray. it should just be a button binding, along with wasd, tab, E, etc.\" Do this in the web client (packages/web): (1) remove the ⚑ \"Plant a flag\" button/form from the Town Hall in-tray (and the building in-tray if it is the same control) so the in-trays show only reports, proposals, checkpoints and flag rows; (2) bind a key for humans alongside WASD / Tab / E in the existing key-binding map (pick a free key, e.g. F) that opens the plant-a-flag box: text + building picker, defaulting to the building the human is standing in; (3) list the key in the same place the other bindings are shown to the human (help/keys legend), and keep the human-only rule (guests/agents never see it). Core (7810e8c) stays as is: POST flag → building in-tray → manager wake → review + assigneeId. Keep tests green, commit straight to main, push, redeploy, verify live on /api/health and in the web bundle; report the commit. Context: plant a flag was built in dc_fj4nfgodwx (core 7810e8c, web 9b20fad) and verified in dc_zc32sjyb2x."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-26T15:50:37.191Z"
createdAt: "2026-10-26T15:49:45.417Z"
updatedAt: "2026-10-26T15:50:37.191Z"
---
the flag feature shouldn't appear in the townhall intray. it should just be a button binding, along with wasd, tab, E, etc.
