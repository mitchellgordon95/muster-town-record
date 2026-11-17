---
id: "dc_nbrxnsk0k9"
type: "report"
state: "building"
title: "PR #489: CI red on docs and knip; fixed, pushed 072a45fd, parked on CI"
authorId: "ag_2slselxix5"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-17T03:56:09.998Z"
sessionId: "se_m6pllbrekl"
assignmentId: "as_ng1md38ks5"
costUsd: 0.4125377
tokens: 20627
turns: 13
createdAt: "2026-11-17T03:56:09.967Z"
updatedAt: "2026-11-17T03:56:09.998Z"
---
## What I did
PR #489 CI failed at check:docs. The cause was a bare test path, `forecast-asks.test.ts`, in docs/invariants/grants.md:66. Locally, check --fast then also failed at knip: `calibratedRatio` and `StepInFlight` in packages/core/src/grant-estimate.ts were exported but used only in that file. I fixed both and pushed commit 072a45fd to the PR branch. The PR is still a draft.

## Findings
- docs: the invariant now cites `packages/core/test/forecast-asks.test.ts`. check-doc-refs passes.
- knip: both symbols are now local to grant-estimate.ts.
- What passed locally: typecheck, and forecast-asks.test.ts (16 of 16). The full core suite already passed on the prior commit (1070 of 1070).
- I have not seen check --fast pass again after the knip fix. Its run was moved to the background and its log stayed empty, so CI decides.
- The pre-push hook did not run because `.githooks/pre-push` is not executable on this desk.
- Not merged yet. Next: if CI is green, mark ready and merge, with no redeploy. If it is red, fix it and park again.

## What I need from you
Nothing needed.
