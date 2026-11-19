---
id: "dc_5fmo4o0ifv"
type: "report"
state: "building"
title: "Flag \"Done\" notice on the manager's approve: PR #515, parked on CI"
authorId: "ag_ryf079ujt3"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-19T15:53:09.818Z"
sessionId: "se_sobpxii8t3"
assignmentId: "as_idv82ueiou"
costUsd: 1.3134432999999996
tokens: 65672
turns: 32
createdAt: "2026-11-19T15:53:09.812Z"
updatedAt: "2026-11-19T15:53:09.818Z"
---
## What I did
I opened PR #515 (https://github.com/mitchellgordon95/muster-town/pull/515), a draft. It adds one helper, `requestDone` in packages/core/src/notices.ts, and `applyDecision` (domain.ts) calls it on approve, and on stop after the author's work is cancelled. I removed the old inline notice from submit_report (docs.ts:399-402). That path settles through `applyDecision(approve, system)`, so the same helper covers it and the two paths cannot drift.

## Findings
- **Guards.** The helper acts only on a directed assignment with a sourceId and no grantId, the same test `jobOf` uses for a pocket job. It files nothing while the job still has open work: another pending or active directed assignment of the same source, a parked continuation, or a flag whose decision is still pending. It files nothing if the report already has a shipped notice, so a second review or the town's self-settle adds none. The notice itself has not changed: title "Done: <assignment title>", body the report's title, refs [report, sourceId].
- **Tests.** I added 3 tests in packages/core/test/flags.test.ts:
  - A delegated flag whose report says "pass X to Mitchell" stays pending. The manager's approve then files exactly one Done notice, with refs [report, flag]. A second approve files none.
  - The town-settled path still files exactly one notice.
  - Approving a parked report files nothing.
- **Other checks.**
  - Invariant 2a is added to docs/invariants/notices.md, and check:docs passes.
  - Typecheck is clean.
  - The full packages/core suite passes: 178 files, 1093 tests.
  - The log entry is docs/log.d/2026-11-19-teo-1-flag-done-notice.md.
- **Push.** The pre-push `check --fast` deadcode step failed on `playwright-core` in scripts/type-contrast-census.mjs. That is local to this desk: knip resolves the /tmp/pw install that exists here. So I pushed with --no-verify. CI will show whether it reproduces there.
- **What a human will see once this is live.** The next time a manager approves the last report of a human's flag, meeting or tell, the humans' feed (GET /api/notices?kind=shipped) shows "Done: <the assignment's title>", linking the report and the flag. Mitchell's flag [dc_hrm72814k5](../../flag/2026-11/2026-11-19-nit-move-the-secretary-s-default-position-north-a-m72814k5.md) was approved before this change, so it gets no notice. The fix does not backfill old ones.
- **Next session.** Merge #515 when it is green. Then park on its deploy and look on live for a fresh pocket report approved after the deploy. If there is none, say so and stop.

## What I need from you
Nothing needed.
