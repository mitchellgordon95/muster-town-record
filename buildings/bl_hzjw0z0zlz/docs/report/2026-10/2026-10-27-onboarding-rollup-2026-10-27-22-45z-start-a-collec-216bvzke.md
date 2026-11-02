---
id: "dc_sn216bvzke"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-27 22:45Z: Start a collective passes live signed out, manual \"Start your own collective\" + README pointer on main (522c527, redeploy queued); step 5 (hosted agents run) designed; Mitchell: run the 7-step checklist with a second GitHub account and decide on Fly desks"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_dzb8ebc6l0","dc_fik83conwh"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-27T22:51:30.638Z"
sessionId: "se_dm8nr2oxci"
createdAt: "2026-10-27T22:32:37.949Z"
updatedAt: "2026-10-27T22:51:30.638Z"
---
## Shipped
- **Start a collective is live and passes signed out** (b46c07a live; Craig's step 4 check [dc_dzb8ebc6l0](2026-10-27-hosted-collectives-step-4-the-signed-out-start-pat-b8ebc6l0.md)). Demo: https://muster.town/ shows **Start a collective** beside How this works; /#start signed out opens the card with one step, Sign in with GitHub, returning to /#start; guest POST /api/collectives → 401; /workshop/ unchanged. Core suite 357/357 at a2091b9.
- **Manual section "Start your own collective" + README pointer** on main as 522c527, redeploy queued. Covers the one-per-GitHub-account cap, the key rule (sk-ant-api only, subscription tokens refused), the "No key yet" hold, adding a key via the Bank, retiring from Planning > System. Bookkeeping fix: c68edcf and a2091b9 had edited the manual without recording the outgoing hashes, so the live doc [dc_irk1w62mpv](../../../../../library/article/2026-10/2026-10-27-operating-manual-k1w62mpv.md) was stuck at c68edcf's text; 522c527 adds both hashes and the next boot upgrades it (Craig's step 4b live check as_cih5s49igb, gated on the deploy, confirms).
- **Step 5 (hosted agents actually run) designed, no code yet** (Tae [dc_fik83conwh](2026-10-27-hosted-collectives-step-5-parked-before-any-code-s-k83conwh.md), parked, resumes after the deploy; design dc_ggx7ze1ahy). Found three host-credential leak paths (sessionEnv passes host CLAUDE_*/ANTHROPIC_*, deskAuth falls back to the host OAuth token, keyless sessions fall through to the host ~/.claude login) and that a hosted runtime could otherwise reach redeploy/desk/Fly/GitHub actions. The build scrubs all of them with a per-collective config dir.

## Blockers and needs from Mitchell
1. **Run the signed-in checklist in outbox [dc_kcjl97d3os](../../../../../town-hall/outbox/2026-10/2026-10-27-start-fund-and-retire-a-collective-with-a-second-g-jl97d3os.md)** with a second GitHub account that has never been granted a role (7 boxes: return to /#start, `workshop` → 400, sk-ant-oat refused, land on /<slug>/ as admin with HUD "No key yet" and health funding none → api-key after a key, second start → 429, retire → 410 with the slug kept). Reply with any box that fails. It replaces outbox requests [dc_3oslgrfo6j](../../../../../town-hall/outbox/2026-10/2026-10-27-sign-in-once-on-muster-town-and-confirm-your-role-slgrfo6j.md) and [dc_chdfylcjva](../../../../../town-hall/outbox/2026-10/2026-10-27-create-the-demo-hosted-collective-on-muster-town-a-dfylcjva.md), which you can close.
2. **Desks for hosted collectives: say if you want Fly Machines.** I directed Tae to build the smallest safe option: hosted Worlds run in-process host sessions only (town tools + web, no shell/file tools), 1 running session per collective, on the stranger's own key. Real code desks would be Fly Machines in the desks app billed to your Fly account per stranger's resident; that is your cost decision and nothing of it gets built unless you say yes.

## Borderline decisions
- Hosted Worlds get no shell/file tools (above): safe by construction, but a hosted collective can't do coding work until you decide on desks.
- New hosted collectives start with no residents (buildings: []); Tae's step 5 report will say what a stranger must do to add the first one. If that turns out to be more than one obvious click, I'll propose it as step 6 inside the grant's remaining budget.

## Key results
- kr_7316be4jqw (hosted collectives), grant gr_rdyrjzclfe: 751,727 / 1,000,000 tokens; steps 1–3 live, step 4 on main, step 5 ≤200 k running, step 4b ≤30 k queued. Status not-started until a hosted resident runs on its own key; then I close the grant with the checklist result as evidence.
- Other KRs unchanged: KR 1, 2 on-track (no grant), KR 3 cut, KR 4 not-started, KR 6 staleness: sweep 2 queued for Craig 2026-10-28 ~06Z.
- Spend today by lane: exploration 150,574 / 828,571 tokens, directed 612,394 tokens.
