---
id: "dc_67jl2y3cqk"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-27 19:20Z: hosted collectives step 1 (the hub) is live on muster.town and passes its checks; step 2 (one sign-in) running; `demo` fixture needs your admin session (outbox)"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_qy0p019gad","dc_86zb0skxge","dc_riz2ypr54e","dc_xu31nhbu1q"],"urls":["https://muster.town/","https://muster.town/api/health","https://muster.town/api/collectives"]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-27T22:49:39.711Z"
sessionId: "se_x76ev9d9al"
createdAt: "2026-10-27T19:08:19.252Z"
updatedAt: "2026-10-27T22:49:39.711Z"
---
## Shipped
- **Hosted collectives step 1, the hub (gr_rdyrjzclfe): live.** Commit 667c72b on main, live as d08fcf9 (Tae's build [dc_86zb0skxge](2026-10-27-hosted-collectives-step-1-the-hub-is-on-main-as-66-zb0skxge.md), Craig's live check [dc_riz2ypr54e](2026-10-27-hosted-collectives-step-1-live-check-the-hub-and-w-z2ypr54e.md)). One process serves the Workshop at /workshop/ and hosted collectives at /<slug>/, each as its own non-listening Fastify app with its own world and session; `POST /api/collectives` (admin-only) brings a new collective up without a restart; hub.db lives in /data/hosted. The old registry.json is gone, the "Coming soon" tile is a constant.
- **Demos:** https://muster.town/ (lists Workshop Collective + Coming soon; screenshot mf_hda13q9nf8), https://muster.town/api/health now has `hosted.count`, https://muster.town/api/collectives lists both; a local /demo/ screenshot is mf_nkz0bwvo4h. Craig's live check: 0 console errors on / and /workshop/, Workshop WS snapshot and town tools unchanged, unknown slug (/demo/) 302s home as designed.
- **Plan cut ([dc_qy0p019gad](2026-10-27-gr-rdyrjzclfe-funded-plan-cut-into-five-grant-lane-0p019gad.md)):** 5 grant-lane steps, hub → live check → one sign-in → Start a collective with the own-key hold → live check + manual + README. Step 2 (one GitHub sign-in across the hub, owner becomes admin of their collective) is with Tae now (as_ezk4dxdxnv, ≤200 k); it parked once so the redeploy could go through ([dc_xu31nhbu1q](2026-10-27-hosted-collectives-step-2-parked-before-starting-s-31nhbu1q.md)) and resumes by itself.

## Blockers and needs from Mitchell
1. **Create the `demo` fixture collective (outbox [dc_chdfylcjva](../../../../../town-hall/outbox/2026-10/2026-10-27-create-the-demo-hosted-collective-on-muster-town-a-dfylcjva.md), 1 minute).** `POST /api/collectives` takes a human admin token; agent tokens get 403, so nobody on the team can make one. The outbox item has the exact console snippet. Optional: if you skip it, the first fixture comes from step 3's Start a collective button and the fixture checks move to step 4.
2. Still pending from the 18:10Z rollup ([dc_umdd6lyamw](2026-10-27-onboarding-rollup-2026-10-27-18-10z-hosted-collect-dd6lyamw.md)): confirm API-key-only as the credential source for hosted collectives (no Claude subscription OAuth).

## Borderline decisions
- Accepted Tae's design change: Fastify refuses routes after listen, so each hosted collective is its own non-listening app that the root app hands requests to (reply.hijack), instead of a prefix registered on one app; the child-process fallback is dropped. Still one process, Workshop untouched. Flag it if you wanted process isolation per collective.
- Craig's unrun checks (fixture creation, `workshop` slug → 400, duplicate → 409) fold into the step 2 live check rather than a new session now.

## Key results
- kr_7316be4jqw (hosted collectives): not-started → on track; gr_rdyrjzclfe at 270,855 / 1,000,000 tokens (step 1 200 k, live check 33 k, plan cut 27 k, parked session 11 k). Steps 2–4 remain (≈600 k planned).
- kr_hee2pa2d5r (staleness): Craig's sweep 2 queued for 2026-10-28 ~06Z (exploration, ≤100 k).
- Spend today by lane: exploration 150,574 / 828,571 tokens; directed 612,394 tokens.
