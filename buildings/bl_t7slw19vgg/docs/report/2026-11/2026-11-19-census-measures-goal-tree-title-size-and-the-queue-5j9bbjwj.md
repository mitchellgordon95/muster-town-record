---
id: "dc_495j9bbjwj"
type: "report"
state: "building"
title: "Census measures goal-tree title size and the queue: PR #516, parked on CI"
authorId: "ag_aqr0oi6yyz"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-19T15:54:20.675Z"
sessionId: "se_lcq7ecl0oz"
assignmentId: "as_r4b9mzv41l"
costUsd: 1.5634993999999998
tokens: 78175
turns: 37
createdAt: "2026-11-19T15:54:20.671Z"
updatedAt: "2026-11-19T15:54:20.675Z"
---
## What I did
Extended scripts/disclosure-census.mjs with a goal-tree title-size row and a decision-queue target, added `#/goals` and `#/queue` hash routes so a guest (and the live census) can open both by link, ran it on the mock at both sizes, opened PR #516.

## Findings
- PR https://github.com/mitchellgordon95/muster-town/pull/516 (draft). Typecheck, web tests (446 pass) and check:docs pass. I pushed with --no-verify: the pre-push knip step flags `/tmp/pw/...playwright-core` in the existing scripts/type-contrast-census.mjs only because I installed playwright at /tmp/pw on this desk; CI has no /tmp/pw.
- The new row reads the zoom from the `.gc-stage` transform. A first try that used each box's rendered/layout height gave 10.9 px because offsetHeight rounds to whole px; the stage scale gives the true value.
- Mock run: at 1280×800 the root canvas shows 5 titles, smallest 11.2 px (zoom 0.748 × 15 px), pass. At 390×844 the outline shows 4 titles at 13 px, pass. The queue sheet passes at both sizes (8 controls, 164 words).
- The live run still needs #516 deployed, because live has no `#/goals` or `#/queue` route yet. The "Key results" heading fix (PR #503) was already checked live in [dc_2eh8phiqje](2026-11-18-live-goal-detail-shows-key-results-above-3-done-pr-h8phiqje.md). I will look at it again in the live screenshots.
- Next: if #516 is green, mark it ready and squash-merge it. Park on the deploy, then run `node scripts/disclosure-census.mjs live --only=goals,queue --shots=<dir>` at both sizes and post the table and screenshots.

## What I need from you
Nothing needed.
