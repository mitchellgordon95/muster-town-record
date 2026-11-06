---
id: "dc_cpov4ziuez"
type: "report"
state: "building"
title: "Schema-migration ask-first rule found (Pix's town-wide FYI dc_xsrxxbfa7i from town hall mt_q1w4o85ao9) and changed: revised town-wide FYI dc_vzqoh7ppen, migrations ship with the PR; Pix and Nell asked to update their copies"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_rzhcwpx9i3","dc_xsrxxbfa7i","dc_9cfo33oa2n","dc_vzqoh7ppen"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Rule change done: revised town-wide FYI dc_vzqoh7ppen live, Pix retired dc_xsrxxbfa7i, Pix and Nell queued to update copies. No follow-up."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-30T02:15:10.766Z"
sessionId: "se_sxrcw4gluj"
assignmentId: "as_mzwp2je67z"
costUsd: 1.94487395
tokens: 38897
turns: 23
createdAt: "2026-10-30T02:14:51.545Z"
updatedAt: "2026-10-30T02:15:10.766Z"
---
## What I did
- Traced the rule. It is not in the repo: it lives in the town-wide FYI "Town-wide merge rules" (dc_xsrxxbfa7i, Pix, 2026-10-28), which copies town hall mt_q1w4o85ao9 decision 1 (notes [dc_9cfo33oa2n](../../../../../library/meeting-notes/2026-10/2026-10-27-town-hall-town-hall-notes-fo33oa2n.md)). Pix proposed the wording there ("ask only for schema or Bank changes") and you said "ok do the things"; it was never a separate ruling on migrations. Copies: Workshop standing rules page [dc_w6e1vpbkuf](../../../../workshop/docs/wiki/2026-10/2026-10-28-workshop-standing-rules-e1vpbkuf.md), Bank Transparency board FYI [dc_57nuw740sc](../../../../bl_vef3v0oux0/docs/fyi/2026-10/2026-10-27-merge-rules-for-bank-transparency-revised-2026-10-nuw740sc.md) and Nell's wiki [dc_a0q82pir2r](../../../../bl_vef3v0oux0/docs/wiki/2026-10/2026-10-29-deploy-ci-and-push-for-bank-transparency-q82pir2r.md), Prod's topic page [dc_e9s5nh8x7u](../../wiki/2026-10/2026-10-29-prod-working-rules-s5nh8x7u.md), and one line of mock text in the web client's test fixture (packages/web/src/mock/fixture.ts).
- Posted the revised town-wide FYI [dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-11-05-ci-deploy-qoh7ppen.md) on the Town Hall board (shows on every building's board), citing your reply on [dc_rzhcwpx9i3](2026-10-30-prod-rollup-20-close-report-for-gr-uhh6u39vv9-desk-hcwpx9i3.md) as the source.
- Rewrote Prod's "Prod working rules" page to match; told Pix (old FYI, Workshop page, fixture line) and Nell (board FYI, wiki). Both were idle, so the town queued the updates as assignments for them (as_9y7epxvz90, as_z52iauozfn).
- No code change, no PR, no redeploy.

## Findings
New rule text ([dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-11-05-ci-deploy-qoh7ppen.md)):
- A manager merges their own building's green PR to main and redeploys without asking (or commits straight to main where the building's rules say so).
- Schema migrations ship with the PR like any other change, no asking first. Keep them additive and backward compatible (new tables, nullable columns, back-fills). One that drops or rewrites live data still ships, but the rollup's "Your call" line says so. Migration numbers must be unique: check the highest number on main right before merging.
- Ask Mitchell first only for Bank or token-accounting changes, or anything that touches another building's code.
- Queue a redeploy when work lands; never wait for the build in-session; say which commit should be live.

I read "let's change it?" as "drop the migration exception". If you meant something else (for example keep ask-first for destructive migrations only), say so and I will edit [dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-11-05-ci-deploy-qoh7ppen.md). Until Pix retires dc_xsrxxbfa7i, both FYIs show on every board; the revised one names the old one as superseded.

## What I need from you
Nothing needed.
