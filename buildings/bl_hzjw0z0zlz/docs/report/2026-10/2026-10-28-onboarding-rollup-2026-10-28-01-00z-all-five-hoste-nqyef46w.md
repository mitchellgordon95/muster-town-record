---
id: "dc_tpnqyef46w"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-28 01:00Z: all five hosted-collectives steps are live and checked; the hosted path now waits on Mitchell's checklist"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_t12ifwxccc","dc_8uka1znx9c","dc_rj70ya3drf","dc_8npkzuqxoo"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-28T16:20:05.208Z"
sessionId: "se_nq66urndqz"
createdAt: "2026-10-28T00:38:06.504Z"
updatedAt: "2026-10-28T16:20:05.208Z"
---
## Shipped
Live on https://muster.town (health commit 1ece19a):
- **Step 4c, c3b6e98** (directed, your 1:1 mt_7eznactr7f decision 2): no tagline; a collective's goal shows under its name on the homepage rows and collective pages; the manual has a "Getting a key" paragraph. Craig's live check [dc_t12ifwxccc](2026-10-27-hosted-step-4c-live-check-all-5-items-pass-on-1ece-2ifwxccc.md): 5/5 pass. Demo: private window on muster.town, the Workshop row shows its goal; HUD "?" → "Start your own collective" → "Getting a key".
- **Step 5, 85ab93b** (gr_rdyrjzclfe): every hosted collective gets its own in-process runtime on its own API key only (POST /<slug>/mcp, scrubbed env, "No key yet" hold in its Bank, one hosted session at a time, hosted redeploy refused with 403). Tae's live check [dc_8uka1znx9c](2026-10-28-hosted-collectives-step-5-live-check-85ab93b-is-li-ka1znx9c.md): health shows runtime true and hosted count 0; the Workshop's Bank and tools are unchanged; docs/hosted-collectives.md matches the code. The hosted path itself (a stranger's collective running a session on their key) cannot be checked from the team: no hosted collective exists yet.

## Blockers and needs from Mitchell
1. **Run the 7-step checklist in outbox [dc_kcjl97d3os](../../../../../town-hall/outbox/2026-10/2026-10-27-start-fund-and-retire-a-collective-with-a-second-g-jl97d3os.md)** with a GitHub account that has never had a role: Start a collective, add a building and a resident, paste an sk-ant key, see a session run. That result is the evidence to close gr_rdyrjzclfe and claim kr_7316be4jqw. Why: the team has no second GitHub account and no key of its own to spend. How: the outbox item lists each step and what you should see.
2. Still open from earlier: the `demo` collective fixture (outbox [dc_chdfylcjva](../../../../../town-hall/outbox/2026-10/2026-10-27-create-the-demo-hosted-collective-on-muster-town-a-dfylcjva.md)) and a real GitHub sign-in check.

## Borderline decisions
- Tae stopped the full core/runtime/server suite re-run on 1ece19a after 12 minutes (a redeploy was waiting on their session) and asked whether to re-run it in its own session. I decided no: the grant has about 25 k tokens left, the step 5 build session ran its hosted test, and the suites will run in the next session that changes hosted-collectives code, before it pushes. Say so if you want a standalone run instead.

## Key results
- kr_7316be4jqw (hosted collectives), grant gr_rdyrjzclfe: 974,437 / 1,000,000 tokens; all five steps live; status stays not-started until a hosted resident runs on its own key (your checklist). The next session on this grant crosses 1 M and writes the checkpoint.
- kr_hee2pa2d5r (staleness): Craig's sweep 2 queued for 2026-10-28 ~06Z (exploration).
- Other KRs: unchanged. Spend today by lane: exploration 0 / 828,571 tokens, directed 0 tokens.
