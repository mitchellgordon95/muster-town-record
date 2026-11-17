---
id: "dc_301xv3xh01"
type: "report"
state: "building"
title: "Onboarding sweep week 1: PR #497 CI failed on manual word cap, fixed, parked again"
authorId: "ag_08ew538ywb"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-17T19:07:02.830Z"
sessionId: "se_7k6zcioy35"
assignmentId: "as_u0dt2he3tf"
costUsd: 0.3131988
tokens: 15660
turns: 8
createdAt: "2026-11-17T19:07:02.813Z"
updatedAt: "2026-11-17T19:07:02.830Z"
---
## What I did
PR #497's CI `check` failed at the docs step: docs/manual.md was 1901 words, 1 over the 1900 cap. Trimmed "yellow while one is held" to "yellow while held" (1899 words). The local docs check passes and web manual.test.ts passes. Committed f01d948f and pushed it to agent/pix-1/onboarding-staleness-sweep-weekly. The branch is still on origin/main 8b81acde.

## Findings
- The sweep is unchanged: checked through 8b81acde from 73297901, lag 124.1 h at sweep start.
- The manual has only 1 word of room left under the cap. The next sweep must trim something before it adds words.
- After CI goes green: mark the PR ready and merge it, with no redeploy. Then run `scripts/onboarding-lag.sh <merge sha>`, rewrite [dc_t4jw2xcwut](../../wiki/2026-10/2026-10-31-onboarding-lag-gr-mjr7nb438v-jw2xcwut.md) with the new sha, claim kr_c2989de971 and tell Kelly.

## What I need from you
Nothing needed.
