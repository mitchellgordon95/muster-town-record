---
id: "dc_ola7jcq561"
type: "report"
state: "building"
title: "Doc-drift check now runs in CI on main: PR #58 merged (49e1647) and main is green"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done: check:docs runs in CI on main. Claim kr_oubxzkl4n6 in the next rollup."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-27T18:52:12.626Z"
sessionId: "se_6478b81dy7"
assignmentId: "as_g4nyii15sl"
costUsd: 0.32631140000000003
tokens: 16430
turns: 14
createdAt: "2026-10-27T18:29:07.192Z"
updatedAt: "2026-10-27T18:52:12.626Z"
---
## What I did
- Merged the latest main into agent/mara/doc-drift-check and ran check:docs and typecheck (both passed). Then pushed.
- The push went through, so the new token has workflow scope.
- Marked PR #58 ready and merged it.
- Approved my earlier report [dc_5pnvzjlnoq](2026-10-27-architecture-grant-first-step-already-with-finn-as-nvzjlnoq.md).

## Findings
- PR #58 is merged into main as commit 49e1647. The CI `check` job now runs `npm run check:docs`, which checks references in README, CLAUDE.md, AGENTS.md, SKILL.md and docs/manual.md.
- CI on the PR passed (run 40559640078). The log shows "doc references ok".
- The CI run on main for 49e1647 passed on its first attempt: https://github.com/mitchellgordon95/muster-town/actions/runs/40559977542
- To check that it can fail, I added a reference to a missing file (`scripts/does-not-exist.ts`) to AGENTS.md on my machine and ran check:docs: it exited with 1. I reverted the change and pushed nothing.
- I haven't tested this with a deliberately broken PR on GitHub.
- This covers kr_oubxzkl4n6. The status update and the claim go in my next rollup.
- A redeploy is waiting for this session to end. This change is CI only and nothing in the running server changes. Main at 49e1647 or later should be live after the redeploy.

## What I need from you
Nothing needed.
