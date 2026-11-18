---
id: "dc_jszddjtfhn"
type: "report"
state: "building"
title: "PR #501 merged: a grant's deciding event retires only its money asks (4b2383a3)"
authorId: "ag_vkvfi6vnsi"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: the exploration found nothing to propose."
decidedBy: "system"
decidedAt: "2026-11-18T00:17:56.433Z"
sessionId: "se_b559mskxpp"
assignmentId: "as_2n4s12zvv0"
costUsd: 0.2149644
tokens: 10748
turns: 5
createdAt: "2026-11-18T00:17:56.428Z"
updatedAt: "2026-11-18T00:17:56.433Z"
---
## What I did
PR #501 passed CI on bb8505d7: `check` and `image` succeeded, and `promote` was skipped, which is normal on a PR. I marked it ready and squash-merged it at 2026-11-18T00:17:48Z as 4b2383a3: https://github.com/mitchellgordon95/muster-town/pull/501

## Findings
- From now on, a deciding event on a grant or retainer retires only the money asks on it. This covers fund, continue, adjust, counter, reject, cut, close, withdraw and stopping. A credential, policy, click, do or meeting card on the same grant or retainer stays live until it gets its own decision.
- The test that pins this: packages/core/test/asks.test.ts › "a grant's or retainer's deciding event retires only its money asks: a credential or policy card on it stays live ([dc_yvgkuk2mv1](2026-11-17-live-moved-to-7a886f88-481-485-live-ci-still-401-a-gkuk2mv1.md))". It is named in docs/invariants/asks.md invariant 3.
- Mara 2 counted 49 asks retired on a grant or retainer deciding event since 2026-11-01. That number is their reading; I did not re-scan.
- The server's prod watcher deploys it once CI promotes main. I did not verify it live this session.

## What I need from you
Nothing needed.
