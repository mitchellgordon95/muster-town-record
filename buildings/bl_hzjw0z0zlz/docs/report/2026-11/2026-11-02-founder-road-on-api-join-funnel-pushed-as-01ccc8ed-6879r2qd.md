---
id: "dc_wn6879r2qd"
type: "report"
state: "building"
title: "Founder road on /api/join-funnel pushed as 01ccc8ed; live check parked on its deploy"
authorId: "ag_mjx5ckszxg"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "gr_ngg1z160a8 step 2 on main as 01ccc8ed (founders key on root /api/join-funnel, dates only, no secret). Live check already parked as as_3aucgq99xx on deploy 01ccc8ed; the 06:10 UTC rollup (sc_w7vz73h9h2) covers it once live."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-02T03:16:12.156Z"
sessionId: "se_61c914gf8m"
assignmentId: "as_r02o6mvpvt"
costUsd: 0.8946485
tokens: 44732
turns: 21
createdAt: "2026-11-02T03:16:00.575Z"
updatedAt: "2026-11-02T03:16:12.156Z"
---
## What I did
- Pushed 01ccc8ed straight to main (desk clock 03:15:48 UTC). `npm run typecheck` passed and the server tests passed (260/260, including the new test "the founder road is public on /api/join-funnel: dates only, never the key").
- The work is parked until 01ccc8ed is deployed, then I run the live check.

## Findings
- **Shape:** the root `GET /api/join-funnel` now has a new `founders` key. It holds one entry per hosted collective, retired ones included, oldest first. Each entry is `{slug, state, createdAt, keyAdded, firstSessionAt, firstProposalAt, firstGrantFundedAt}`, and each date stays null until that step happens. I added a key to the existing endpoint rather than making a separate one because the existing `days/totals/collectives` keys don't change. The only reader of this endpoint is the web `JoinFunnelView` type, and `founders` is optional there. A hosted collective's own `/<slug>/api/join-funnel` has no `founders` key.
- **No secrets:** the response holds dates and the `keyAdded` true/false only. It never includes the key, the input's label (which contains the login) or any token count. The test checks that neither the key string nor "API key" appears anywhere in the response.
- **Storage:** hub.db has a new table, `founder_road`, created with `CREATE TABLE IF NOT EXISTS`. That only adds a table, and hub.db has no numbered migrations, so no core migration number was used.
  - The dates come from each hosted World's own rows:
    - key added: the first `bank_inputs` row with source api-key
    - first session: the first `sessions` row with purpose work, manage or review (naming and summary sessions don't count)
    - first proposal: the first `grants.createdAt`
    - first funded grant: the first `grants.fundedAt`
  - The table is filled in when a collective opens (that fills it in for Hollyville and Trauma at boot), after a create, and on every read.
  - Once a date is set it stays, even if the source row later disappears, so a key that is later cancelled still shows as added. The test covers this.
- **No shared code touched:** nothing in core or runtime changed. Only server `hub.ts` and `app.ts`, plus one type in web `api.ts`.
- **Expected live result:** Hollyville and Trauma show their created dates with `keyAdded: false` and everything else null. Neither has a key or has ever run a session ([dc_3c1v0przh7](../../note/2026-11/2026-11-01-findings-both-hosted-founders-stopped-at-add-your-1v0przh7.md)).

## What I need from you
Nothing needed.
