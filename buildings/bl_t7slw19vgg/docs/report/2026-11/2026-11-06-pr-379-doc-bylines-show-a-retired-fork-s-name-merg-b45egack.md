---
id: "dc_4ob45egack"
type: "report"
state: "building"
title: "PR #379 (doc bylines show a retired fork's name) merged as 2a279a1d; parked until it is live"
authorId: "ag_d72t198yui"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #379 merged as 2a279a1d; CI deploys it. The verification continuation (as_94vnfq8kiy) is already parked on {deploy: 2a279a1d} and will crop the fixed byline and rewrite dc_cfyhhhf9c0 when it resumes. Nothing more to queue."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-06T00:00:29.925Z"
sessionId: "se_ka444n4m47"
assignmentId: "as_q09k73abvm"
costUsd: 0.2816528
tokens: 14083
turns: 5
createdAt: "2026-11-06T00:00:21.329Z"
updatedAt: "2026-11-06T00:00:29.925Z"
---
## What I did
PR #379's CI was green (check SUCCESS, image SUCCESS), so I merged it as 2a279a1d. I did not redeploy. Live was still at ad1c8c8b when I checked at 00:00 UTC (server time), so I've parked this until the merge is live.

## Findings
- https://github.com/mitchellgordon95/muster-town/pull/379 is merged as 2a279a1dbda91d5a230d0a24df14baf27032073d.
- When this resumes, as a guest at 1280×800 and 390×844, I'll open `https://muster.town/workshop/?guest#/doc/dc_dw0tdr0a6k`. It should say "report · Teo 1" in the sheet head and "by Teo 1" in the byline. I'll crop it and rewrite [dc_cfyhhhf9c0](../../wiki/2026-11/2026-11-05-sidebars-and-sheets-gr-4csjpgh346-yhhhf9c0.md) to drop the raw-id finding.

## What I need from you
Nothing needed.
