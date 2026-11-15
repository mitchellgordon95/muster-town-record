---
id: "dc_efe080qamh"
type: "report"
state: "building"
title: "Secretary's request-card rewrites now hold: PR #452 open, parked on CI"
authorId: "ag_kksz2al6uj"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-15T19:12:05.777Z"
sessionId: "se_3thx401s31"
assignmentId: "as_ux4csst7by"
costUsd: 0.5574084
tokens: 27870
turns: 13
createdAt: "2026-11-15T19:12:05.763Z"
updatedAt: "2026-11-15T19:12:05.777Z"
---
## What I did
Fixed the revert of the Secretary's rewrites on request-backed ask cards (Mitchell, 1:1 mt_t65exni4et). Opened draft PR https://github.com/mitchellgordon95/muster-town/pull/452 and parked on its CI.

## Findings
- **Fix.** In `packages/core/src/asks.ts` `townCardOf`, captain, access and request asks now return null once their history has a `rewritten` entry. `rewriteAsk` is the only writer of that entry, and only the Secretary can call it. After that, `rerenderAsks` keeps the Secretary's words and its `renderedSeq`, so `entriesSinceCard` marks the card as behind when its thread moves. Proposals, gates and retainers are unchanged. I updated the doc comment above `rerenderAsks` to say so. The log line is in docs/log.d/2026-11-15-pix-secretary-rewrite-holds.md.
- **Tests** in packages/core/test/ask-snapshots.test.ts:
  1. A rewritten request card keeps its title and body through a new thread entry and through a boot pass. `entriesSinceCard` goes from 0 to 1, and `rerenderAsks` returns 0. Without the fix this test fails; with it, it passes.
  2. A request card nobody rewrote is still re-rendered from its doc.
- **Checks run.** These test files pass: ask-snapshots (7), asks (10), ask-checks, ask-contract, secretary-rank, secretary and forecast-asks. `npm run typecheck` is green. It first failed because my desk was missing `fast-check`; `npm install` fixed that, and the lockfile did not change.

## What I need from you
Nothing needed.
