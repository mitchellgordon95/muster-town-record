---
id: "dc_7xmu43qhfc"
type: "report"
state: "building"
title: "PR #259 CI failed on main's own check breakage; fixed on the branch, waiting on CI again"
authorId: "ag_mpdi72uq4u"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Main's own check breakage (manual 23 words over the cap, 3 unused exports) fixed on the PR #259 branch as 64f5170; the continuation is parked on CI. Nothing new queued: merge, redeploy and the rollup 38 line stay with the parked continuation; step 2 as_jr1thl80jr waits on it."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-02T03:22:07.287Z"
sessionId: "se_xblelj1kzq"
assignmentId: "as_l3oe8cqb93"
costUsd: 0.5758621999999999
tokens: 28793
turns: 15
createdAt: "2026-11-02T03:21:31.154Z"
updatedAt: "2026-11-02T03:22:07.287Z"
---
## What I did
PR #259's CI (head 1c8f714) failed after 20 s in `scripts/check.ts` docs. The cause was main, not the PR: Mitchell's commits f72fe63 and 88bcbf3 left main failing its own check. I merged main into the branch and fixed main's breakage there (commit 64f5170). The full check passed locally, I pushed the fix and marked the PR ready. It is waiting on CI again: https://github.com/mitchellgordon95/muster-town/pull/259

## Findings
- **Two problems on main:**
  - docs/manual.md was 1923 words, 23 over the 1900-word cap.
  - knip (the dead-code check) flagged 3 unused exports: `HOSTED_CAP_LINE` in BankFunding.tsx, and `HelpThing` and `HelpCard` in helpCard.ts.
- **Every PR's CI fails on these until something merges a fix.**
- **Fix in 64f5170:**
  - I trimmed the manual to 1896 words without dropping any facts. I cut wording only: the long "host your own…" link text, "who can do what", the outbox examples, "over the building", and "for humans".
  - I removed `export` from the three symbols.
- **Local result:** the full check passed (docs, deadcode, typecheck 42 s, tests 6 m 38 s).
- **The PR's own content is unchanged** (captain gates, tests, docs/goals.md). Nothing is merged or live yet.
- **Note for step 2 (as_3pqax4qf1m):** the manual is now 4 words under its cap. Any captain lines added to it need a trim first.
- Topic page [dc_ooe47kx4un](../../wiki/2026-11/2026-11-01-captain-steering-rights-e47kx4un.md) is rewritten with this state.

## What I need from you
Nothing needed.
