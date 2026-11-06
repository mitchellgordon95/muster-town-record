---
id: "dc_hz1nz88pkt"
type: "flag"
state: "building"
title: "i'd like to be able to rename my collective"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag dc_hz1nz88pkt: \"i'd like to be able to rename my collective, specifically \"Trauma\" to \"Trauma Town\". idk if we want to change slugs once we create the town though, so maybe some decoupling there if not already.\" Ship a rename for a hosted collective that leaves its slug alone. What the code says today (snapshot 1edf24d): hub.db `collectives` keeps slug (PRIMARY KEY, the address /<slug>/) and name as separate columns (packages/server/src/hub.ts:87-95), the slug only defaults to slugify(name) at create (hub.ts:188), and `create` also writes the name into <dir>/collective.json and the hosted World's own town row (hub.ts:201, seed; the HUD shows town.name, packages/web/src/hud.tsx:229; the homepage tile reads the hub row, packages/server/src/home.ts:25). There is no rename route: `POST /<slug>/api/collective/retire` (app.ts:62, api.ts:889) is the only collective-level mutation. Build: (1) a route for the collective's admins (its owner; hosted apps have admins: [] + ownerGithubId, main.ts:118) that renames the collective, e.g. PATCH /<slug>/api/collective {name} (and tagline/goal if cheap), updating the hub row, collective.json and the World's town row in one go, slug untouched; (2) a small UI way to do it from the hosted town (an admin control near the town name in the HUD or the collective settings, whatever exists), and from the Workshop root as the hub admin if that's cheap; (3) tests in packages/server/test. Mitchell owns \"Trauma\": once your PR is live, either rename it yourself if an API path lets a root admin do it, or say in your report exactly where he clicks. Keep the slug fixed (say so in the UI: \"the address muster.town/trauma stays\"). Merge your own green PR; CI deploys main (no `redeploy`); report the merge commit and park on {deploy: sha} only if you need the live check. Separate assignment handles the Hollyville deletion."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T18:57:30.886Z"
flagPos: {"x":124,"y":28}
pickedUpAt: "2026-11-05T18:56:43.327Z"
pickedUpBy: "ag_mh0qidzgw6"
createdAt: "2026-11-05T18:56:22.146Z"
updatedAt: "2026-11-05T18:57:30.886Z"
---
i'd like to be able to rename my collective

specifically "Trauma" to "Trauma Town"

idk if we want to change slugs once we create the town though, so maybe some decoupling there if not already

also can you delete Hollyville it was just a test
