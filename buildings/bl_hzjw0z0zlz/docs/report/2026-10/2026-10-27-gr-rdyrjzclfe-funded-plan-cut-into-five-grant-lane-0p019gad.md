---
id: "dc_qy0p019gad"
type: "report"
state: "building"
title: "gr_rdyrjzclfe funded: plan cut into five grant-lane steps, step 1 (the hub: one process hosts many collectives at /<slug>/, Workshop untouched) assigned to Tae as as_dsf55wxj7p (≤350 k); next steps assigned one at a time from each report"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_umdd6lyamw","dc_evzrmyl3pp","dc_d1i9awyh9l"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Plan cut acknowledged; step 1 (hub) runs with Tae as as_dsf55wxj7p. Step 1b live check and later steps get assigned from Tae's report. Folds into the next rollup (when step 1 is live)."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-27T18:22:43.581Z"
sessionId: "se_pkyg2mxxzy"
assignmentId: "as_8qc08xcpe2"
costUsd: 2.098709
tokens: 26525
turns: 13
createdAt: "2026-10-27T17:53:50.700Z"
updatedAt: "2026-10-27T18:22:43.581Z"
---
## What I did
Read the funded grant gr_rdyrjzclfe, docs/hosted-collectives.md (b6e1379) and the live server code it changes (packages/server/src/main.ts, app.ts, context.ts, home.ts; packages/web/src/api.ts; deploy/README.md), then cut the plan into steps of one session each and assigned step 1 to Tae in lane grant. No code of my own this session. A redeploy (the one queued for b6e1379) was waiting on my session; it goes out when this report lands.

## Findings
**The cut** (all lane grant gr_rdyrjzclfe, 1,000,000 tokens; each next step is assigned from the previous step's report, never ahead, so a design surprise in step 1 can change step 2):

| Step | Owner | Budget | Human check in the live town |
|---|---|---|---|
| 1. Hub: one process hosts many Worlds, hub table replaces registry.json, /<slug>/ mounts, web client reads its base at runtime, admin-only POST /api/collectives | **Tae, as_dsf55wxj7p (assigned now)** | ≤350 k | /api/health has the sha and `hosted.count`; /workshop/ loads signed-out with 0 console errors; /api/collectives served with no registry.json on main; a Workshop resident's session after the deploy ends with a report (Craig's sweep 2 ~06Z is the proof) |
| 1b. Live check of step 1 | Craig or Tae, waitFor {deploy: sha} | ≤40 k | the rows above, at 1400×900 and 390×844 |
| 2. One sign-in: root OAuth callback, root cookie, hub users table, creator = admin | Tae (Permissions wiki) | ≤200 k | sign in once at /, open /<slug>/, /<slug>/api/me knows you |
| 3. Start a collective: homepage form, POST open to signed-in users, reserved/taken slugs refused, one per user, own-key hold (empty credential env, agents held "No key yet"), retire | Craig (style-guide work) | ≤300 k | private window, never-granted account: form → muster.town/<slug>/ as admin under 5 min; / lists it; held session shows the no-funding notice |
| 4. Live check with a second GitHub account, manual section "Start your own collective", README pointer | Craig | ≤100 k | /workshop/#/manual lists the section; README's section names muster.town |

**Why Tae for step 1**: idle with nothing queued, and Tae's wiki covers home.ts and the server test layout from the KR 3 build PR; Craig's queue holds sweep 2 (2026-10-28 ~06Z) and the sweep report doubles as step 1's "Workshop agents still work" proof.

**Design facts I put into the assignment so step 1 does not stall**: the Fly volume is /data with the Workshop at /data/workshop, and the town's `redeploy` only pulls main and restarts (no `fly deploy`), so the hosted dir must derive from MUSTER_TOWN_DATA (`/data/hosted`), not from a new env var; `app.decorate("world")` on the root instance is what blocks multi-World, so the fix is one encapsulated Fastify plugin per collective with its own `app.world`, auth hook and interact gate, the Workshop at prefix "" so the root /api, /ws, /mcp stay as they are; the web client calls absolute /api and location.host/ws, so it needs one runtime base derived from the first path segment. Hosted Worlds boot with no runtime in step 1 (sessions, the own-key hold and retire are step 3). The fallback if the single-process hub proves too invasive stays the grant's: one child process per collective behind a reverse proxy, same URLs; Tae reports early in that case and I decide before step 2.

**Spend**: this session ≈ 25 k of the grant; step 1's ceiling leaves ≈ 600 k for steps 1b to 4.

Rollup: none now ([dc_umdd6lyamw](2026-10-27-onboarding-rollup-2026-10-27-18-10z-hosted-collect-dd6lyamw.md) filed minutes ago, decision pending). Next rollup when step 1 is live, with the screenshots Mitchell asked for.

## What I need from you
Nothing needed.
