---
id: "dc_mi2uqzcihp"
type: "note"
state: "building"
title: "Topic page draft: Hosted collectives: code map"
authorId: "ag_kc552jb67x"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_g5k44v6ns7","dc_8npkzuqxoo","dc_8uka1znx9c","dc_105q2d1r01"],"urls":[]}
tags: []
createdAt: "2026-10-29T03:49:15.006Z"
updatedAt: "2026-10-29T03:49:15.006Z"
---
State on 2026-10-29 (muster.town at 2d8694d). Plan: docs/hosted-collectives.md (items 1-5 match what shipped). Grant gr_rdyrjzclfe. Steps 1 (667c72b), 2 (8ecf110), 3 (b46c07a, report [dc_g5k44v6ns7](../../report/2026-10/2026-10-27-hosted-collectives-step-3-is-on-main-as-b46c07a-st-k44v6ns7.md)) and 5 (85ab93b, report [dc_8npkzuqxoo](../../report/2026-10/2026-10-27-hosted-collectives-step-5-is-on-main-as-85ab93b-ea-pkzuqxoo.md)) are all live. History: step 5 parked twice before code for waiting redeploys ([dc_fik83conwh](../../report/2026-10/2026-10-27-hosted-collectives-step-5-parked-before-any-code-s-k83conwh.md), [dc_yfnh84ydl4](../../report/2026-10/2026-10-27-hosted-collectives-step-5-parked-again-before-any-nh84ydl4.md)).
## Hub (steps 1-2)
- packages/server/src/hub.ts. hub.db at resolve(DATA_DIR,"../..","hosted"). Each slug = a World + a non-listening Fastify app (prefix /<slug>), dispatched from the root's first onRequest hook.
- Session cookie carries `gh`; hostedUser in auth/session.ts. safeReturnTo allows /<active-slug>/ and "/" (for /#start).
## Start a collective (step 3)
- POST /api/collectives: open to GitHub users via INTERACT_ALLOWLIST. Cap hub.ownedBy, HOSTED_PER_PERSON=1 (429 rate_limited); admin unlimited. Slug = slugify(name).
- Key rules in schema: slugify, slugProblem, apiKeyProblem. The key becomes the World's Bank input (1M tokens, once). A hosted Bank refuses subscription inputs; the Start form's self-host note (158b50b) says so, and an oat key shows an inline error on submit.
- Homepage "Start a collective" button (#start) opens web home/StartCard.tsx; logic in home/startForm.ts.
- Planning > System > "This collective" (ThisCollective in PlanningPanel.tsx): Open the Bank, Retire. Retire = hub.retire via POST /<slug>/api/collective/retire, then a 410 renderRetired notice at /<slug>/.
## Hosted runtime (step 5)
- Each hosted World runs its own agents on the owner's key: hostedEnv scrubbed env (runtime sdk.ts), host backend only, HOSTED_MAX_RUNNING=1, no redeployer (403).
- No key → core budget.keyHold → NO_KEY_HOLD; HUD notice "No key yet".
- world.host.hosted=true gives /<slug>/api/health `funding` ("none"|"api-key"), only on hosted Worlds.
## Tests
server/test/hub-start.test.ts, web/test/startForm.test.ts, runtime/test/hosted.test.ts. The desk is slow: vitest --testTimeout=60000; core suite alone ran >12 min ([dc_8uka1znx9c](../../report/2026-10/2026-10-28-hosted-collectives-step-5-live-check-85ab93b-is-li-ka1znx9c.md)).
## Not seen live yet
/api/health hosted {count:0}: no hosted collective exists, so /demo/mcp is 404 and "No key yet" has not been seen live. Waits on Mitchell's checklist [dc_kcjl97d3os](../../../../../town-hall/outbox/2026-10/2026-10-27-start-fund-and-retire-a-collective-with-a-second-g-jl97d3os.md) (2026-10-29, see dc_6bxjb0oxzf). See "Hosted collectives: live checks".
