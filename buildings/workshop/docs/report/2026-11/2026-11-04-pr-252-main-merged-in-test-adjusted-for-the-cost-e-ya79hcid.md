---
id: "dc_hfya79hcid"
type: "report"
state: "building"
title: "PR #252: main merged in, test adjusted for the cost-estimate session, parked on CI"
authorId: "ag_rh47zn1yy8"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. Continuation as_i6r5ftrrde waits on {pr: 252} (merge if green, redeploy); as_5sa92hqqjd (keyed live-check outbox request, rollup-43 line) follows the park chain and holds until that lands (waits.ts chainTip). Rollup 43 at the 02:30Z wake."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T00:55:59.877Z"
sessionId: "se_8rbdyvbirq"
assignmentId: "as_km3xgpu8j1"
costUsd: 0.5481545000000001
tokens: 27408
turns: 15
createdAt: "2026-11-04T00:55:41.628Z"
updatedAt: "2026-11-04T00:55:59.877Z"
---
## What I did
I merged main into PR #252 (https://github.com/mitchellgordon95/muster-town/pull/252). The only conflict was in docs/log.md, and I resolved it. After the merge one assertion in hub-explore.test.ts failed, so I fixed it and pushed the result as head 31cd2e1d. I also rewrote the topic page [dc_pl034gahw2](../../wiki/2026-11/2026-11-01-hosted-collectives-first-run-034gahw2.md).

## Findings
- **Why the assertion failed:** main now runs a grant cost-estimate session when a proposal is filed (eb42fa5e). That session records `credentialInputId` (the founder's key input) but `funding: null`. The test now checks:
  - every session ran on the key input;
  - every session other than estimate and naming has funding `api-key`;
  - an estimate session ran.
  The billing behaviour itself is unchanged.
- **Local results:** the server suite passes 273/273 and typecheck is green.
- **Not merged yet:** CI has not run on the new head, so I parked on {pr: 252}. Once it is green I merge and redeploy.
- **Rollup item 14:** its text is unchanged from [dc_uu60h4svq6](2026-11-01-hosted-step-3-traced-keyed-collective-s-first-tick-60h4svq6.md), and the manager pastes it. The PR is test-only, so it needs no live check of its own. The keyed live check (Your call) is still Mitchell's.

## What I need from you
Nothing needed.
