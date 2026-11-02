---
id: "dc_vpbhfzf20o"
type: "report"
state: "building"
title: "Hosted collectives API-key only is live (PR #202, 289e865 in 00bf7ff); Hollyville reports funding \"none\""
authorId: "ag_sad06i5nur"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_nzjrxs1zf2","dc_32xbgegtvn"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/202"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. PR #202 (hosted collectives never run on a subscription, directed from mt_p3ge56kg03) is live at 00bf7ff; Hollyville reports funding \"none\" as expected. Goes into the next rollup as a \"Your call\" item. Its follow-on as_v143vxiefm (recurring API-key donations limited to N credits) is now free to run."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-31T21:48:22.278Z"
sessionId: "se_4vm4tn0k2h"
assignmentId: "as_dt1nfqsh8j"
costUsd: 0.4913442
tokens: 24567
turns: 12
createdAt: "2026-10-31T21:48:09.674Z"
updatedAt: "2026-10-31T21:48:22.278Z"
---
## What I did
Mitchell had already merged PR #202 (https://github.com/mitchellgordon95/muster-town/pull/202) at 21:31:48Z as merge commit 289e865, and CI deployed it. I didn't need to merge it or call redeploy. I checked the live server and rewrote topic page [dc_32xbgegtvn](../../wiki/2026-10/2026-10-31-one-credential-per-session-and-the-daily-funding-r-xbgegtvn.md). My session branch was not used.

## Findings
- **Live:** `GET /api/health` at 21:47:24Z reported commit 00bf7ff (server started 21:41:53Z). `git merge-base --is-ancestor 289e865 00bf7ff` succeeds, so the change is live.
- **Hosted collective:** `GET /api/collectives` lists one hosted collective, `hollyville`. `GET /hollyville/api/town` returns health.funding = `"none"`, which is the expected result. `/hollyville/api/bank` has no inputs, so no stray subscription row exists and no migration is needed.
- **Workshop:** `GET /api/town` has no `funding` field, so the Workshop still runs on its subscription as before.
- **What I did not check live:** the hosted hold message and the Donate form without a subscription option. Hollyville has no inputs to trigger them. The tests in PR #202 cover both (core bank.test.ts, runtime hosted.test.ts, web hostedDonate.test.tsx).
- **For the rollup:** "Your call" line: a Bank/credential change that Mitchell asked for himself in 1:1 mt_p3ge56kg03. In a hosted collective, subscription inputs are refused and a session runs on the Bank's API key or is held. The Workshop and self-hosted towns are unchanged.

## What I need from you
Nothing needed.
