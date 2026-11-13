---
id: "dc_nbb34tu32g"
type: "report"
state: "building"
title: "Pure-core design line merged: PR #446 → 6ea6b60e, AGENTS.md rule 8 on main"
authorId: "ag_dp32351ahq"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: the request is done."
decidedBy: "system"
decidedAt: "2026-11-13T06:12:48.691Z"
sessionId: "se_05rs4oiu5k"
assignmentId: "as_iy949jwdiz"
costUsd: 0.255671
tokens: 12784
turns: 6
createdAt: "2026-11-13T06:12:48.686Z"
updatedAt: "2026-11-13T06:12:48.691Z"
---
## What I did
PR #446's CI came back green: the check and image jobs passed, and promote was skipped as it always is on PRs. I squash-merged it and deleted the branch. I did not call redeploy, because CI deploys main by itself.

## Findings
- **Merge commit:** 6ea6b60e ("AGENTS.md rule 8: pure core, stateful shell (mt_msnjkpgwdb decision 15) (#446)"). It is the tip of origin/main.
- **Rule 8 is on main:** AGENTS.md line 29 holds Standing Rule 8, "Pure core, stateful shell". docs/architecture.md line 358 links to it in one line. Line 359 adds fast-check to the allowed dependencies (dev only, added by the first PR that has a pure core). I checked both with `git show origin/main:<file>`.
- **What a human checks:** open AGENTS.md on main and find "Pure core, stateful shell" in Standing Rules.
- The other pieces of decision 15 are separate assignments. The chain-of-command transform is as_fts38a0zxd; it adds fast-check. The Bend 2 findings doc is already filed as [dc_lsmeci1asz](../../note/2026-11/2026-11-13-bend-2-for-the-town-s-pure-cores-findings-and-reco-meci1asz.md).

## What I need from you
Nothing needed.
