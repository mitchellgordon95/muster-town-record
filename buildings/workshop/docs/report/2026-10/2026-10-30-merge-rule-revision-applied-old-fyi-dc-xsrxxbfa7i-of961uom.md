---
id: "dc_whof961uom"
type: "report"
state: "building"
title: "Merge rule revision applied: old FYI dc_xsrxxbfa7i retired, standing rules dc_w6e1vpbkuf rewritten, fixture text merged (71176a2, PR #110)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_rzhcwpx9i3","dc_vzqoh7ppen","dc_xsrxxbfa7i","dc_w6e1vpbkuf"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/110"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Merge rule revision fully applied: old FYI retired, standing rules rewritten, fixture merged as 71176a2 (PR #110, mock only). Decided-only for rollup 31."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T02:17:07.899Z"
sessionId: "se_5rup6p83t9"
assignmentId: "as_9y7epxvz90"
costUsd: 1.4134271999999999
tokens: 28269
turns: 18
createdAt: "2026-10-30T02:16:46.799Z"
updatedAt: "2026-10-30T02:17:07.899Z"
---
## What I did
Mitchell's reply to Prod rollup #20 ([dc_rzhcwpx9i3](../../../../bl_xvgnd1fvh6/docs/report/2026-10/2026-10-30-prod-rollup-20-close-report-for-gr-uhh6u39vv9-desk-hcwpx9i3.md)) changed the merge rule: schema migrations no longer need asking first; ask-first stays only for Bank/token-accounting changes and another building's code. Cleo posted the revised town-wide FYI [dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-11-05-ci-deploy-qoh7ppen.md) and asked me to bring the Workshop's three copies in line. All three are done and Cleo is told (ms_6qz3ddnjmb).

## Findings
- **Old town-wide FYI dc_xsrxxbfa7i retired.** Set back to draft and retitled "(retired 2026-10-30; superseded by [dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-11-05-ci-deploy-qoh7ppen.md))" with the original text kept for the record. Checked the Workshop board afterwards: only Cleo's revised FYI and Mitchell's "Prefer shipping immediately" note remain town-wide. No duplicate rule shows on any board.
- **Workshop standing rules [dc_w6e1vpbkuf](../../wiki/2026-10/2026-10-28-workshop-standing-rules-e1vpbkuf.md) rewritten** (revision 3). Bullet 3 now reads: ask Mitchell first only for Bank/token accounting or another building's code, citing [dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-11-05-ci-deploy-qoh7ppen.md). A new bullet says migrations ship with the PR (additive, backward compatible; destructive ones flagged in the rollup's "Your call"; unique numbers).
- **Web mock fixture updated.** packages/web/src/mock/fixture.ts line 110 (sample FYI "Town-wide merge rules") now carries the revised wording. Typecheck passed (49 s). PR #110 https://github.com/mitchellgordon95/muster-town/pull/110 merged to main as 71176a2. Mock data only, so no redeploy was queued; the next redeploy carries it.
- Grepped docs/, README.md and collective.json for the old "ask first for schema migrations" wording: no other copies in the repo.
- Rollup 31: this report is Decided-only (no Shipped item; a rule change, not a feature).

## What I need from you
Nothing needed.
