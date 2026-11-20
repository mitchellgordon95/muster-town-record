---
id: "dc_vfrr4gdlp9"
type: "wiki"
state: "building"
title: "Ask cards readable at a glance (gr_x7p580xe1o)"
authorId: "ag_m6fa1edhwy"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_t7slw19vgg"
createdAt: "2026-11-20T01:49:50.113Z"
updatedAt: "2026-11-20T18:28:21.952Z"
---
State 2026-11-20 18:30 UTC (Teo 2). Grant gr_x7p580xe1o closed (all three KRs met; PRs #530, #533). Its mid-card buttons were then undone on Mitchell's word (1:1 mt_gf4un6ct4p, 18:14 UTC: "put them all back together at the bottom"): PR #542, parked to merge when green (as_aqsosz9n1z).

- Card order after #542 (AskCard.tsx): header, title, deferred stamp, lead (`.ask-delta`, weight 600), recommendation, the whole rest of the body (`.ask-body`, weight 400, line breaks on; its "If you <branch>:" sentences stay where the author wrote them), step strip, claims, then ONE `.ask-actions` row, last on the card: AskButtons (counter / adjust / note form opens under them), the aside, Steer, "The full record →". Signed out: the row holds "Sign in to decide." (`.ask-signin`) plus the record.
- Removed in #542: asks.ts `splitConsequences`, the `consequences` prop, `.ask-branch/.ask-conseq/.with-conseq/.ask-branches-static/.ask-foot`. Kept: 56ch, line-height 1.5 on lead, body and recommendation; `deltaOf` (lead = first paragraph if a blank line, else first sentence; tests in packages/web/test/askLead.test.ts). `data-branches` stays on the `<article>`.
- Census ask-card row: `node scripts/disclosure-census.mjs mock|live --only=queue [--shots=dir]` at 1366×800 and 390×844. Pass: body weight 400, ≤1 bold block, ≤80 chars/line (laptop), recommendation top < 844 (phone), and at both sizes the decision row is the card's only and last block with every button inside it. Mock 18/18 on #542; screenshots mf_afwdyqff0o (laptop), mf_2dpyl5z4ql (phone). Live not yet rerun after #542.
- Kelly (ag_s1n1xknj8n) was told to update the ask-card section of muster-style-guide ([dc_q736158pnn](../../../../bl_hzjw0z0zlz/docs/skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md)): buttons bottom, no consequence split; the "label's first word" writers' rule is no longer needed for layout.
