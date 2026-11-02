---
id: "dc_1hm8dk92ba"
type: "report"
state: "building"
title: "Hosted collectives step 2 live-checked as guest: Hollyville has a Workshop and its manager Dev; the bundle carries the keyless HUD line"
authorId: "ag_5utix5eobn"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_pm8nse129m","dc_7lpbltjy1j","dc_pl034gahw2"],"urls":["https://muster.town/api/health","https://muster.town/hollyville/api/town"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 2 live-checked as guest; kr_god7otzibq claimed at the checkpoint (rollup 37)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-02T02:20:52.507Z"
sessionId: "se_xaq0372kcu"
assignmentId: "as_eaqtna926x"
costUsd: 0.9300025000000002
tokens: 46500
turns: 26
createdAt: "2026-11-01T21:26:03.979Z"
updatedAt: "2026-11-02T02:20:52.507Z"
---
## What I did
Ran the guest live check for PR #242 (= 6e876b7, gr_5ltmbf3a2f step 2, kr_god7otzibq). Took a guest screenshot of Hollyville with headless Chromium. Added item 13 to the rollup page [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md) and set item 11 (#248) to LIVE, since it is merged as 9c2d894 and that commit is in the live build. Rewrote [dc_pl034gahw2](../../wiki/2026-11/2026-11-01-hosted-collectives-first-run-034gahw2.md). I changed no code and opened no PR.

## Findings
- **Health:** read at 2026-11-01T21:23:53Z. The live commit is be51fee (started 21:23:28Z), and 6e876b7 is in it (`git merge-base --is-ancestor` passed). hosted.count = 2.
- **GET /hollyville/api/town:** lists the Town Hall plus bl_ue25sk4oaq "Workshop".
  - The Workshop is a lab on gl_town, goal-directed, with headcount 5. It was created 21:23:28Z, at this boot, as `ensureFirstBuilding` does on reopen.
  - Its manager is Dev (ag_la2d1ivd3f), a resident on Fable, idle, with 0 tokens spent so far. Ada is in the Town Hall.
- **Bundle:** /workshop/assets/main-CiNhzXwk.js contains `"Add your API key to start"` followed by ": your agents wait until the Bank has one". That text only shows for an admin; a guest sees the "Watch first" panel instead.
- **Picture:** mf_24d26po5b6, a live guest view of the Hollyville minimap showing Town Hall + Workshop, cropped to 300 px. The main view opens on the Town Hall, so the Workshop only shows on the minimap.
- **KR status:** kr_god7otzibq can be claimed. kr_n2zh7s6s2s was already claimable.
- **Step 3 (kr_f722z9ut50):** not started. It needs a collective that has a key. Hollyville has none.

## What I need from you
Nothing needed. Item 13's "Your call" asks Mitchell to start a throwaway collective without a key from the homepage, to see the admin HUD line.
