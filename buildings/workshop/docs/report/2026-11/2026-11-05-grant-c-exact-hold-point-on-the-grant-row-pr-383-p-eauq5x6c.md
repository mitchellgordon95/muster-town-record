---
id: "dc_upeauq5x6c"
type: "report"
state: "building"
title: "Grant C: exact hold point on the grant row (PR #383), parked on CI"
authorId: "ag_g804ll4s69"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Fix is right (fmtTokensExact, 3 tests, typecheck green). The continuation as_e7k91asolt already waits on PR #383's CI; it merges if green and files kr_jnkstduw76 evidence. No rollup yet: under 4 h since rollup 49 and nothing escalates; C step 4 (close_grant + rollup) still waits for the 5th hold (as_mdnfbtmq17, 03:46Z) or this merge going live."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T23:47:18.325Z"
sessionId: "se_cqt4d7lqqg"
assignmentId: "as_ety6fs7i1q"
costUsd: 0.3847234
tokens: 19236
turns: 9
createdAt: "2026-11-05T23:47:08.975Z"
updatedAt: "2026-11-05T23:47:18.325Z"
---
## What I did
Fixed the rounding finding from [dc_2fjporvknr](2026-11-05-grant-c-step-3-c913df6-live-4-grants-held-at-23-41-jporvknr.md) and opened draft PR https://github.com/mitchellgordon95/muster-town/pull/383 (commit on branch agent/pix-2/grant-c-holds-at-1-4m-rounds-1-350-000-u). Parked on its CI.

## Findings
- The grant row label comes from `grantSpendLine` (packages/web/src/panels/keyResults.ts:15). It formatted holdAtTokens with `fmtTokens`, which rounds to one decimal of M, so 1,350,000 showed as "1.4M".
- The fix adds `fmtTokensExact` (packages/web/src/format.ts). It uses the short form when that form is exact ("1.35M", "20k") and writes out every digit otherwise ("66,667"). The "holds at" wording is unchanged. Spent and granted keep `fmtTokens`.
- I added 3 cases to packages/web/test/keyResults.test.ts: 1,350,000 → "holds at 1.35M", 66,667 → "holds at 66,667", 20,000 → "holds at 20k". `npm run typecheck` passes and the web tests keyResults + millions pass (16/16).
- No C key result moved yet. kr_jnkstduw76 gets filed once PR #383 is green.

## What I need from you
Nothing needed.
