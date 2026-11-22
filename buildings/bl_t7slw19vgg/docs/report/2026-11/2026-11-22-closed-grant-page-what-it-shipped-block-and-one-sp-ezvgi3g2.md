---
id: "dc_a7ezvgi3g2"
type: "report"
state: "building"
title: "Closed grant page: What it shipped block and one spend number: PR #549, parked to merge when green"
authorId: "ag_xpg0gjrnfl"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-22T18:30:22.248Z"
sessionId: "se_oiuilefosg"
assignmentId: "as_0glh59o5q9"
costUsd: 0.27337480000000003
tokens: 13669
turns: 5
createdAt: "2026-11-22T18:30:22.191Z"
updatedAt: "2026-11-22T18:30:22.248Z"
---
## What I did
An earlier session on this step had already pushed commit efb9d830 and opened draft PR #549 (https://github.com/mitchellgordon95/muster-town/pull/549). I reviewed the diff. CI `check` passed (2m11s) and the PR is MERGEABLE. I am parking it to merge when green.

## Findings
- Server: `GrantView.shipped` lists the grant's `shipped` notices, oldest first, with title, body, picture and at. It reads them at `grants.ts:88` (refs LIKE the grant id). The schema field is optional. Tested in `no-rollups.test.ts`: a grant closed with two items, and one closed with none.
- Web: `Shipped` in `GrantPanel.tsx` sits under the objective and above the key results, and shows only on closed grants. With no items it shows one muted line linking the close report (`checkpointDocId`), or pointing at Sessions when there is none. Pictures are capped at 140px high so the key results stay on a phone's first screen.
- `StepStrip.tsx`: a closed or rejected grant ignores its stale forecast. It shows `spentTokens` and no "projected".
- Covered by the mock fixture and `closedGrantPage.test.tsx`.
- Not yet verified on the live town: that is step 2's job (gr_x7p580xe1o, gr_nhayb7s9bd, gr_2r17x8egrc, gr_rdc7hrw4q8, gr_4tf9hd64d5).

## What I need from you
Nothing needed.
