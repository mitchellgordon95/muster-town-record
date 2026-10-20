---
id: "dc_0f9ib5xlu7"
type: "report"
state: "building"
title: "Turns on report rows and header — PR #3 (stacked on #1, #2)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_9wdhjxr64t","dc_lu58fne2xn"],"urls":["https://github.com/mitchellgordon95/agent-town/pull/3","https://github.com/mitchellgordon95/agent-town/pull/2","https://github.com/mitchellgordon95/agent-town/pull/1"]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Workshop standup\": Pix: after #3, open a small web-only PR so reviewers can approve from the Reports row, gated on store.can(\"…review\"). Check it in a browser, and note in the PR"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-20T01:48:53.171Z"
sessionId: "se_r6rxx47uz9"
assignmentId: "as_1qdkx3awyy"
createdAt: "2026-10-20T00:59:28.761Z"
updatedAt: "2026-10-20T01:48:53.171Z"
---
## Summary
Yes, report docs should carry `turns`, and Root's PR #2 already does it: it adds `Doc.turns`, migration 004, and `finishWorkSession` stamps tokens/costUsd/turns onto the report. I added the web part. Draft PR https://github.com/mitchellgordon95/agent-town/pull/3: `docCost` now renders `$x.xx · N tokens · T turns` on Reports-tab/board rows and in the DocView byline. PR #3 is stacked: its branch merges #1 and #2, so reviewers should look at the last commit only.

## What I did
- Read Root's report dc_9wdhjxr64t and the diffs of PR #1 and PR #2.
- Merged both branches into mine. The only conflicts were appended lines in docs/log.md, and I kept all of them.
- `packages/web/src/panels/DocView.tsx`: `docCost` adds `T turns` ("1 turn" when singular). Each part is skipped when missing.
- Added the first web unit test, `packages/web/test/docCost.test.ts` (3 cases), plus a line in docs/log.md.

## Findings
- Verification: `npm run typecheck` passes. `npm test` passes in all packages (web 3/3, runtime 22/22, others green). I reverted the DocView change and re-ran: 2 of the 3 new tests fail, so they test the change.
- Screenshot description (not captured, since the desk has no browser): a row reads `Pix · 3m ago · $0.61 · 108k tokens · 42 turns`. Reports without usage render as before.
- Inference: reports written before #2 merges have no `turns`, so they show only cost and tokens. Nobody plans a backfill.
- Housekeeping: my checkout started with uncommitted changes I didn't make (package-lock.json, a desk/cli.ts mode change). They're in `git stash` and not committed.

## Proposal for next session
Can a reviewer approve a pending report from the Reports-tab row, without opening DocView?
Why: my direction says "fewer clicks to review". Right now review takes open → scroll → act. Sources: `packages/web/src/panels/DocView.tsx` (Act buttons), the Agent panel's Reports tab, and `store.can("…review")`. If rows already have the needed data and permissions, it's a small web-only PR.

## For others
- Merge order: #1 → #2 → #3. After #1 and #2 merge, #3's diff is one function, one test and one log line.
- packages/web now has a `test/` dir that vitest picks up. Pure helpers can be unit-tested there.

## Questions for humans
- Is stacking by merging a sibling PR's branch acceptable, or would you rather I wait for merges and rebase-free re-branch from main?
