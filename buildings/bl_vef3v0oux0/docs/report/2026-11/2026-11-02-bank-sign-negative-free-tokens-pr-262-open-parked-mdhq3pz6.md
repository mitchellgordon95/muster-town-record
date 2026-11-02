---
id: "dc_oymdhq3pz6"
type: "report"
state: "building"
title: "Bank sign negative free tokens: PR #262 open, parked on CI"
authorId: "ag_cbtcycs0m2"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #262 (Bank sign FREE = freeTokens − overdraftTokens, red when negative; flow title card + legend same; bank-sign test) open and parked on CI. Continuation as_hjj3h2xh89 already waits on {pr: 262} (merge on green, redeploy, live check + picture), so approve only. Expected live reading after deploy: −712,236."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-02T03:20:23.235Z"
sessionId: "se_w293nvalls"
assignmentId: "as_43pubcxy4v"
costUsd: 0.41804700000000006
tokens: 20902
turns: 10
createdAt: "2026-11-02T03:20:14.708Z"
updatedAt: "2026-11-02T03:20:23.235Z"
---
## What I did
Implemented Mitchell's flag [dc_jlqnc3d36r](../../flag/2026-11/2026-11-02-i-think-we-can-show-overdraft-as-negative-free-tok-qnc3d36r.md) in PR https://github.com/mitchellgordon95/muster-town/pull/262: the Bank marquee's FREE column shows `freeTokens − overdraftTokens` with a real minus sign (U+2212), drawn red when negative. The flow view's title card ("… free") and its legend "Free" row showed the same number, so they changed the same way. I added two helpers, `netFreeTokens` and `signed`, to format.ts. Core's zero clamp is unchanged. I added a test to bank-sign.test.ts: with overdraft 400 the sign draws "−400".

## Findings
- Typecheck passes and the web tests pass (238/238) on my desk.
- Live GET /api/bank right now: freeTokens 0, overdraftTokens 712,236 across 5 funded grants, including gr_4tf9hd64d5 at 200,000. After the deploy the sign should read **−712,236**.
- Parked on CI. Next session: merge on green, call redeploy, then check the sign signed out and take one cropped picture (playwright per skill [dc_hzqgqqeqho](../../skill/2026-10/2026-10-29-screenshot-live-town-qgqqeqho.md)). The report from that session says which commit is live.

## What I need from you
Nothing needed.
