---
id: "dc_ws2l7kwaa6"
type: "report"
state: "building"
title: "goals.test.ts migration-061 flake fixed: PR #311 merged (8a9034c)"
authorId: "ag_lv56y4enfy"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done: PR #311 merged (8a9034c), test-only, no redeploy needed. Flake fixed by moving the 061/069 migration tests to in-memory SQLite."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-04T18:10:40.729Z"
sessionId: "se_bmha80cj56"
assignmentId: "as_k52kupw32i"
costUsd: 0.3233454
tokens: 16167
turns: 8
createdAt: "2026-11-04T18:10:35.360Z"
updatedAt: "2026-11-04T18:10:40.729Z"
---
## What I did
PR #311's CI passed on head 7cad33b (run https://github.com/mitchellgordon95/muster-town/actions/runs/41883336026; the check job ran 18:04:09–18:07:37Z). I marked the PR ready and merged it: https://github.com/mitchellgordon95/muster-town/pull/311 → main **8a9034c**. It only changes test code, so I did not queue a redeploy.

## Findings
- **Before:** "migration 061" in goals.test.ts used an on-disk SQLite file. It took 5,446 ms on CI run 41865260373, which is over vitest's 5 s timeout, so it failed. On the desk it took 131–147 ms. Its twin "migration 069" in grants-schema.test.ts took 638 ms on CI and 135–148 ms on the desk.
- **After:** both tests now use `:memory:` SQLite. On the desk 061 takes 70–73 ms and 069 takes 79–86 ms. Neither writes to disk any more, so a slow CI disk can no longer push them past the timeout. Both passed in the PR's CI. The CI log does not show per-test times (the vitest reporter leaves them out), so I don't have a CI number for after the change.
- v12.test.ts still uses a disk file. It has to, because World.open reopens the database by its path. I left it alone.
- The work is done.

## What I need from you
Nothing needed.
