---
id: "dc_gicoqg3f5r"
type: "note"
state: "building"
title: "Topic page draft: Hosted collectives (gr_rdyrjzclfe) live state"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_60qzrvrqa4","dc_riz2ypr54e","dc_9oka3bqhxb","dc_dzb8ebc6l0","dc_cy2ntbmslj","dc_rj70ya3drf","dc_t12ifwxccc","dc_kcjl97d3os"],"urls":[]}
tags: []
createdAt: "2026-10-29T03:49:35.692Z"
updatedAt: "2026-10-29T03:49:35.692Z"
---
State on 2026-10-29 (live 2d8694d; health shows runtime:true, hosted.count 0). Grant gr_rdyrjzclfe, KR kr_7316be4jqw: a signed-in stranger starts a collective at muster.town/<name> from the homepage.
## What is live (steps 1 to 5, all passed live checks)
- Step 1 (667c72b): the hub. `/` lists collectives as tiles; the Workshop opens at /workshop/.
- Step 2 (8ecf110): one GitHub sign-in for the whole hub, with return_to back to the collective you came from.
- Step 4 (b46c07a) + 4b (522c527): the Start a collective card (signed-out path passes live), manual section "Start your own collective", README pointer.
- Step 4c (c3b6e98): no tagline any more. Tiles and the HUD show the goal under the name (the Workshop's from collective.json, the placeholder's from its goal text). The Start card has Name, Goal and an optional key field; the key hint links support article 17154008; manual has "Getting a key". Town.tagline stays only in the schema/seed and CLI; the web src reads it only in mock/fixture.ts.
- Step 5 (85ab93b): a runtime per hosted World.
## What is not checked yet
- The signed-in path (create `demo`, become its admin) needs a human session: an agent token gets 403. Checklist for Mitchell: outbox [dc_kcjl97d3os](../../../../../town-hall/outbox/2026-10/2026-10-27-start-fund-and-retire-a-collective-with-a-second-g-jl97d3os.md) (step-2 sign-in check [dc_3oslgrfo6j](../../../../../town-hall/outbox/2026-10/2026-10-27-sign-in-once-on-muster-town-and-confirm-your-role-slgrfo6j.md)). Scheduled with Mitchell for 2026-10-29 with a fresh GitHub account (town FYI dc_6bxjb0oxzf); Kelly closes the grant on the result. Don't ask again.
## How to check
- health `hosted.count` goes above 0 once `demo` exists; GET / shows the new tile; muster.town/<name>/ shows that name and goal.
- Bundle greps as in the Live verification page.
## Sources
Live checks [dc_riz2ypr54e](../../report/2026-10/2026-10-27-hosted-collectives-step-1-live-check-the-hub-and-w-z2ypr54e.md) (step 1), [dc_9oka3bqhxb](../../report/2026-10/2026-10-27-hosted-collectives-step-2-live-check-8ecf110-is-li-ka3bqhxb.md) (step 2), [dc_dzb8ebc6l0](../../report/2026-10/2026-10-27-hosted-collectives-step-4-the-signed-out-start-pat-b8ebc6l0.md) (step 4), [dc_cy2ntbmslj](../../report/2026-10/2026-10-27-hosted-collectives-step-4b-522c527-live-check-all-2ntbmslj.md) (4b), [dc_rj70ya3drf](../../report/2026-10/2026-10-27-hosted-step-4c-on-main-as-c3b6e98-tagline-dropped-70ya3drf.md) + [dc_t12ifwxccc](../../report/2026-10/2026-10-27-hosted-step-4c-live-check-all-5-items-pass-on-1ece-2ifwxccc.md) (4c, 5).
