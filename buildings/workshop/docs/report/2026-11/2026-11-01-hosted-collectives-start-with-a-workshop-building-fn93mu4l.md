---
id: "dc_y3fn93mu4l"
type: "report"
state: "building"
title: "Hosted collectives start with a Workshop building and an \"Add your API key to start\" step: PR #242, parked on CI"
authorId: "ag_16dgdz4yw8"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 2 of gr_5ltmbf3a2f built; continuation chain (as_lmb4qf4bsh → CI fix ee7c820) already running. Human live check (Start a collective without a key) goes in rollup 37 \"Your call\"."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-01T02:21:46.949Z"
sessionId: "se_uzmtix99p3"
assignmentId: "as_q5vonvpjqm"
costUsd: 1.6383635
tokens: 81918
turns: 39
createdAt: "2026-11-01T02:15:10.986Z"
updatedAt: "2026-11-01T02:21:46.949Z"
---
## What I did
Built kr_god7otzibq (gr_5ltmbf3a2f step 2) in PR https://github.com/mitchellgordon95/muster-town/pull/242. Head is 4d15b41, with main 08c16a7 merged in. The PR is marked ready, not draft, because I merge it myself. I'm parked on its CI.

## Findings
- **Server (`packages/server/src/hub.ts`):** `hub.open` now calls `ensureFirstBuilding(world)`. A World with no building besides the Town Hall gets one goal-directed lab named **Workshop**, attached to gl_town. It is made through the same path as Planning → New building (`ops.createBuilding(null, {name})`): its manager sits at a desk with free desks beside it, forks are on, and code access follows the collective defaults (off in a hosted World). Because it runs in `open`, it covers new collectives and also Hollyville, which gets its building at the next boot. Buildings are never deleted, so this fires once per World.
- **HUD (`packages/web/src/hud.tsx`):** I reused the existing keyless notice, which shows when `health.funding === "none"`. The collective's admin now sees **Add your API key to start** ("your agents wait until the Bank has one") with a link to the Bank. Others still see "No key yet". Once a key is added, funding becomes `api-key` and the line disappears. There is no setting or flag.
- **Tests:** in `hub-start.test.ts`, after Start, `/api/town` lists one lab, Workshop, on gl_town with code access off. Its manager is a resident at one of its desks, headcount is above the desks in use, and a keyless collective has funding `none`. With a key it has funding `api-key` and still exactly one building. In `hub.test.ts`, a Hollyville-style World with only a Town Hall gets the building on reopen, and a restart doesn't add a second one.
- **Checks:** `npm run check --fast` is green (typecheck, docs, tests), except one backup.test worker-timing test that failed under load and passes when run alone (23/23).
- **Docs:** hosted-collectives step 5 "First building" is rewritten (the merge conflict with Onboarding's 3e3cbdd is resolved in favour of the seed). I also updated architecture.md, manual.md (now 1,895 of its 1,900-word cap) and log.md.
- **Root goal text:** a fresh hub World's root still reads "The town goal", not the Start form's goal. That belongs to Step 1 (kr_n2zh7s6s2s, the parallel fork). My test doesn't assert it.
- **Left for the next session:** merge, redeploy, then a guest live check: GET `/hollyville/api/town` lists Workshop and a resident, `/api/health` commit contains the merge, and the bundle carries "Add your API key to start". After that I'll post the Shipped candidate on [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md). Topic page [dc_pl034gahw2](../../wiki/2026-11/2026-11-01-hosted-collectives-first-run-034gahw2.md) is rewritten with the current state.
- **Needs a human for the live check (for the rollup's "Your call"):** a guest can't see a hosted admin's HUD. Mitchell, or a test account, would sign in at muster.town and press **Start a collective** with no API key. He should land on `/<slug>/` with a **Workshop** building on the map and the HUD line **Add your API key to start**. Its Bank → opens the Bank. After adding a key there, the line goes away. The collective can then be retired from Planning → System → This collective, but its slug stays taken.

## What I need from you
Nothing needed.
