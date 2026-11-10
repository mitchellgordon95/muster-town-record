---
id: "dc_db426sd9dr"
type: "report"
state: "building"
title: "Clipped prose-ask titles: cause found, PR #404 fixes the parser and retitles live asks at boot; waiting on CI"
authorId: "ag_nhce2kyed3"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Cause found (retitleClippedAsks at migration 105 cut titles at first colon/comma and 8 words, not the parser). PR #404 (proseAskTitle, retitleProseAsks boot repair, invariant 12) waits on CI; the continuation as_5n62pzk6q8 is already parked on {pr: 404} to merge and check /api/asks live. Nothing else to queue; rollup when it is live."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-09T23:23:08.838Z"
sessionId: "se_m39qnczsbj"
assignmentId: "as_8padylmm8t"
costUsd: 1.7344591000000005
tokens: 86723
turns: 35
createdAt: "2026-11-09T23:23:01.149Z"
updatedAt: "2026-11-09T23:23:08.838Z"
---
## What I did
Read the live /api/asks (23:05Z): 9 open asks filed from rollup prose. Traced where the clipping comes from, fixed it, added a boot repair and tests, and opened draft PR https://github.com/mitchellgordon95/muster-town/pull/404 (branch agent/pix-1/fix-clipped-titles-of-click-and-credenti). main has not moved since 9e3db116, and there is no migration in the PR.

## Findings
- **The cause was not the parser.** `asksFromRollupProse` titled asks `clipWords(call, 160)` (packages/core/src/asks.ts:428). The asks filed at the 04:05Z backfill had "…" titles. At 15:30Z the migration-105 repair `retitleClippedAsks` ran `proseCardOf`, which calls `nameWithin(title, 120)` and then `grantTitleOf` (packages/schema/src/grant-title.ts). That cut each title at its first comma, colon or semicolon, and to 8 words. This is where the bad titles came from:
  - "A 1" came from the colon in "1:1".
  - "Optional" came from "Optional:".
  - "Continue" came from "Continue, adjust or cut".
  - "Create one empty repo under dungeonrpg99-ops and give", "Step 3 will rewrite AGENTS.md non-negotiable 1 and" and "A tell or @mention to a manager with" were all cut at 8 words.
  - Separately, a long line filed at creation was cut mid-phrase at 160 characters: ak_emigaxsalm ends with "so".
- **Fix (PR #404):**
  - New schema function `proseAskTitle`. It takes the whole first sentence and drops markdown and parenthesised asides (ids, file:line). It never cuts a sentence that fits at a colon. A sentence over 160 characters is cut at its last clause boundary (`;`, `:` or a dash, then a comma, then before "so/and/but"), never in the first third. Only if none of those exist does it cut at a word.
  - `asksFromRollupProse` now uses it. Its idempotency check also matches the source line, so a retitled ask gets no twin from the backfill.
  - New boot repair `retitleProseAsks`, run in world.ts after `retitleGrantAsks`. It finds live prose-read asks (rollup source, a "From … the rollup" body, the prose branches, no recommendation or claims) and gives each one its title again from its own source line. Body, sources, rank and status are kept, and a "retitled" history entry is added. Typed asks from a manager are untouched. It is idempotent.
  - Added invariant 12 to docs/invariants/asks.md.
- **Run on the live source lines**, the three examples become:
  - "A 1:1 with Juno when you have time, as you said in your 1:1 with Secretary"
  - "Optional: give the test account dungeonrpg99-ops "direct work under" the Onboarding goal so a fork can check the stranger's 1:1 path"
  - "Create one empty repo under dungeonrpg99-ops and give MUSTER_TEST_GH_TOKEN Contents read/write on it"
  - "Continue" becomes "Continue, adjust or cut the three held Workshop grants from their cards in your in-tray".
- **Checks run locally:** typecheck, core 898/898 (new test/prose-ask-titles.test.ts), server 304/304, knip and check:docs all pass. I changed one existing assertion: the prose title no longer ends with a period.
- Still to do: merge once CI is green, then check /api/asks after the deploy. Topic page [dc_rdx7am7r9q](../../wiki/2026-11/2026-11-09-grant-titles-and-how-asks-name-a-grant-x7am7r9q.md) is updated.

## What I need from you
Nothing needed.
