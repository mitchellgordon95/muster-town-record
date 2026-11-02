---
id: "dc_ks5la608go"
type: "report"
state: "building"
title: "KR 3 (README walk) closed out: Tae's held walk cancelled, new key result kr_7316be4jqw (a signed-in stranger starts a collective at muster.town/<name> from the web) and grant gr_rdyrjzclfe (1,000,000 adjusted tokens) proposed; Mitchell: fund, counter or reject it in the Town Hall in-tray"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_z4zgfk6tsz","dc_be4b0urgjc","dc_grpkt74cku"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done. The grant decision and the deletion of kr_tzg9en02dh are Mitchell's; both go into this rollup's Needs from Mitchell."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-27T04:03:40.088Z"
sessionId: "se_n4iv43i80x"
assignmentId: "as_hsg160mt74"
costUsd: 3.35406545
tokens: 59945
turns: 27
createdAt: "2026-10-27T04:03:17.590Z"
updatedAt: "2026-10-27T04:03:40.088Z"
---
## What I did
Carried out decision 4 of the Town Hall meeting ([dc_z4zgfk6tsz](../../../../../library/meeting-notes/2026-10/2026-10-27-town-hall-town-hall-notes-zgfk6tsz.md)): Mitchell cut key result 3 (a stranger runs their own Muster Town from README.md) and its grant gr_ibccoje227 (now `closed` on the live server, 289,904 / 266,667 adjusted tokens spent).
- Cancelled Tae's held walk continuation as_sq6dx2fozp (the resume of the blind README walk at 3:26). Tae's only queued work is now the directed live check of the operating manual (as_cwj6zalrl5, waits for Craig's as_4y6ifkyyy5). Craig's manual build is untouched.
- Wrote the new key result **kr_7316be4jqw** on the Onboarding goal: a signed-in stranger starts their own collective from the web at muster.town/<name>, no clone and no server of their own; within 5 minutes of Start a collective they are its admin at muster.town/<name>/, it is listed on the homepage, the Workshop at /workshop is untouched. How to check: private window, GitHub account never granted a role, stopwatch.
- Proposed **gr_rdyrjzclfe** for it: 1,000,000 adjusted output tokens (≈ 30 M raw at 30:1; for scale, the stranger-path grant spent ≈ 525 k adjusted and the README-walk grant 290 k). It is in the Town Hall in-tray.
- Wiki: closed the "README walk (KR 3)" page, started "Hosted collectives (KR 5)" (dc_lyleug3a13).

## Findings
What the grant has to change (read from main at ec6ae2c): today one process is one collective. `packages/server/src/main.ts` opens a single World (one SQLite DB, one port), every route reads `app.world`, the web base is the constant `/workshop/` in `server/src/context.ts` and the Vite build, and prod (fly.town.toml) pins `collectives/workshop`. The homepage list is `collectives/registry.json`, read per request. Sign-in is per collective (session cookie per port, users table in the collective's DB, one GitHub OAuth callback per app).

The plan in the proposal, four PRs to main in order, each with tests and a redeploy:
1. Hub: many Worlds in one process, each collective its own DB at /data/<slug>/data, routes, ws and mcp mounted under /<slug>/ with a Fastify plugin per prefix; root /api, /ws, /mcp keep pointing at the Workshop so agents, desks, the CLI and old links are untouched; web base read from the URL at runtime.
2. One sign-in at the root for all collectives (hub users table, linked by githubId per collective, visitor-until-let-in per collective, creator is admin).
3. Start a collective on the homepage: name, goal, tagline; POST /api/collectives seeds and mounts it live and redirects to /<slug>/; one per GitHub user; reserved and taken slugs refused; a hosted collective never spends the host's Claude token (sessions held with a notice unless its own Bank is funded); admin retire route.
4. Live check with a second GitHub account, manual section "Start your own collective", README pointer.
Stop condition: the key-result check passes live, the Workshop is unaffected, the host token is never spent by a hosted collective; or tokens are out. Out of scope: desks and funding for hosted collectives' agents (I'd make that the next key result), custom domains. Fallback if the single-process hub is too invasive: one child process per collective behind the hub as a proxy.

Open points flagged in the proposal note: (a) anyone signed in may start one collective (my default) versus needing Mitchell's Let in first; (b) running agents in a hosted collective is left for the next key result; (c) the old kr_tzg9en02dh still shows on the goal with status on-track until a human deletes it.

## What I need from you
Fund, counter or reject gr_rdyrjzclfe in the Town Hall in-tray, and delete the old key result kr_tzg9en02dh from the Onboarding goal.
