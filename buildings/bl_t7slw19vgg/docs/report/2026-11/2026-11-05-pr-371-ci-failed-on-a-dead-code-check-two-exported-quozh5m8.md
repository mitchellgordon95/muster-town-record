---
id: "dc_vbquozh5m8"
type: "report"
state: "building"
title: "PR #371 CI failed on a dead-code check (two exported helpers); fixed, CI re-running; parked"
authorId: "ag_o3obfmufp1"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked on {pr:371}; the continuation as_2v4g8h2xd4 merges when green. Nothing else to do here."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-05T20:41:52.629Z"
sessionId: "se_srqq7ddoh7"
assignmentId: "as_1bk9eprvpf"
costUsd: 0.37215909999999996
tokens: 18608
turns: 8
createdAt: "2026-11-05T20:41:41.409Z"
updatedAt: "2026-11-05T20:41:52.629Z"
---
## What I did
CI on PR #371 (https://github.com/mitchellgordon95/muster-town/pull/371) failed at `check: deadcode`. Two helpers in `panelResize.tsx`, `savedSideWidth` and `saveSideWidth`, were exported but only used inside that file. I made them private and pushed the fix as 293f64ff. On my desk, typecheck passes and all 342 web tests pass. I'm parked until CI finishes on the new commit.

## Findings
- The PR's code is otherwise unchanged. The Bank and the goal editor still share one Sheet component.
- `npm run check` on my desk also reports `playwright-core` as an unlisted dependency in `scripts/type-contrast-census.mjs`. That file is already on main. CI's knip run on the same file didn't flag it, so I think this only happens on my desk because of local setup, and I left it alone.
- Next: once CI is green, mark the PR ready, merge it (no redeploy) and park until the merge is live. Then check the Bank on live as a guest and report with the crops mf_m8ve20l835 / mf_mjkwtjkwx7.

## What I need from you
Nothing needed.
