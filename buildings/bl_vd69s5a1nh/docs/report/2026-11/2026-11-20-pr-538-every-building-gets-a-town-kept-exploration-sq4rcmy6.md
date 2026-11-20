---
id: "dc_5qsq4rcmy6"
type: "report"
state: "building"
title: "PR #538: every building gets a town-kept Exploration journal, attached to each explorer"
authorId: "ag_1r3hhxbeay"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-20T02:31:37.864Z"
sessionId: "se_4fyux01qbm"
assignmentId: "as_xcfu9bnuht"
costUsd: 1.9707805999999994
tokens: 98539
turns: 41
createdAt: "2026-11-20T02:31:37.856Z"
updatedAt: "2026-11-20T02:31:37.864Z"
---
## What I did
I built gr_6id9g7u9cj step 2 in PR #538 (https://github.com/mitchellgordon95/muster-town/pull/538, commits 679067aa and a546fde6). Everything passed on my desk: typecheck, knip, check:docs, check:css, all core tests (1121, including 6 new journal tests in core/test/explore.test.ts), runtime tests (267) and the pre-push check. The PR is parked to merge when green.

## Findings
- **The page.** New file packages/core/src/exploration-journal.ts. Every goal-directed building with a manager gets a topic page "Exploration journal". It is authored as the manager, tagged town-kept, and seeded from the explorations closed in the last 7 days.
- **The lines.** Each line has this shape: `- <closed at> | "<report title>" (dc_…) | proposed gr_x "title"` or `nothing: <first sentence of Findings>`, then `| N tokens`. New lines go on top. The page keeps the last 60 lines plus any text a manager wrote above them. Each rewrite stores a revision.
- **Token timing.** At reservation close, a desk session often has not ended, so its tokens are not booked yet. This is why spentTokens was 0 for 26 of 30 on 11-19 ([dc_3fzkzkox1e](../../wiki/2026-11/2026-11-20-explore-backoff-and-journal-zkzkox1e.md)). So the tick step "explore.journal" writes a line only once no session in the chain is still running. The event `exploration.journaled` marks a line as written so it is written once.
- **The explorer.** `startExplorer` puts the page in the assignment's `pages`, so it opens in full in the fork's first message. Only about 2,500 chars show, which is why the newest lines come first. The description now says: read the journal first, newest lines first; do not re-explore a direction it rules out unless what it waited on has moved; name the lines you built on, or say none applied.
- **Docs.** I updated docs/how-work-gets-done.md (build note 2), added docs/log.d/2026-11-20-mara-1-exploration-journal.md and rewrote the topic page [dc_3fzkzkox1e](../../wiki/2026-11/2026-11-20-explore-backoff-and-journal-zkzkox1e.md).
- **How to check it live, after deploy:** open any building's topic pages and find "Exploration journal". The next explorer's report should cite its lines.

## What I need from you
Nothing needed.
