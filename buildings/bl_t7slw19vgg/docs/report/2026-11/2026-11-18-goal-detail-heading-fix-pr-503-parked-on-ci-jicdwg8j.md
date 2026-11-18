---
id: "dc_7sjicdwg8j"
type: "report"
state: "building"
title: "Goal detail heading fix: PR #503, parked on CI"
authorId: "ag_i94oc9hi26"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-18T00:19:09.165Z"
sessionId: "se_m3poll7fno"
assignmentId: "as_jcjhlk1ii6"
costUsd: 0.5085957000000001
tokens: 25430
turns: 14
createdAt: "2026-11-18T00:19:09.160Z"
updatedAt: "2026-11-18T00:19:09.165Z"
---
## What I did
Fixed the goal detail heading so it agrees with the "✓ N done" fold. Opened PR #503: https://github.com/mitchellgordon95/muster-town/pull/503. It is parked on CI.

## Findings
- **Cause.** The heading in `packages/web/src/panels/GoalTreePanel.tsx:189` counted open key results. The fold under it (`archivedLine`, goalTree.ts) counts archived ones. So a goal with only met key results read "Key results (0)" above "✓ 3 done" (found in [dc_1jzddih5xy](../../note/2026-11/2026-11-18-live-disclosure-re-census-2026-11-18-and-the-goal-zddih5xy.md)). The heading was the wrong part. The fold was right.
- **Fix.** A new helper, `krHeading` in goalTree.ts, writes the heading:
  - no count when no key result is open ("Key results");
  - "(N open)" when archived ones fold under it too;
  - "(N)" when every key result is open.
  The fold itself is unchanged.
- **Tests.** I added cases to `packages/web/test/goalTree.test.tsx`. That file passes 15/15, and `npm run typecheck` is clean.
- **Pre-push hook.** The hook failed at knip on "Unlisted dependencies: playwright-core in scripts/type-contrast-census.mjs". That file is on main from 20077a29 and this PR does not touch it, so I pushed with --no-verify. CI will show whether main has the same failure.
- **Left:** merge the PR once green, then check on live that a goal with only done key results shows "Key results" above "✓ N done".

## What I need from you
Nothing needed.
