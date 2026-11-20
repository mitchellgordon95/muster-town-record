---
id: "dc_k5mohfvfdm"
type: "report"
state: "building"
title: "Hydrant water arcs into a small pool, not at the Secretary: PR #529, parked to merge when green"
authorId: "ag_9mqbf0zed6"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-20T01:43:21.157Z"
sessionId: "se_8zywxul2cg"
assignmentId: "as_51l4g59xk6"
costUsd: 1.1581031000000002
tokens: 57905
turns: 32
createdAt: "2026-11-20T01:43:21.147Z"
updatedAt: "2026-11-20T01:43:21.157Z"
---
## What I did
Mitchell's flag [dc_umioej89iy](../../flag/2026-11/2026-11-20-i-don-t-understand-why-the-water-coming-out-of-the-ioej89iy.md). PR https://github.com/mitchellgordon95/muster-town/pull/529 changes `packages/web/src/map/hydrant.ts` and `renderer.ts` drawStream, adds tests in `packages/web/test/hydrant.test.tsx`, adds a 2026-11-20 line to docs/legible-delegation.md §3 A, and adds docs/log.d/2026-11-20-hydrant-pool.md.

## Findings
- **What a human sees at the hydrant now:** water-blue dots leave the hydrant's right side outlet. Each rises about half a tile on a parabola and falls into a small pool on the floor tile to the right. The Secretary is no longer the target. The code also drops the `secretaryOf` lookup.
- **The pool still shows how much is waiting.** It is 4 px wide with no open asks and grows to one tile (16 px) at 12 asks (`poolWidth`). With no asks it stays as a puddle with no dots. With reduced motion the pool still shows but there are no dots.
- **Side:** the pool goes on the floor tile east of the hydrant, or west if east is not floor. Live layout: hydrant at (2,6), Secretary at (3,3), so the pool sits 3 tiles below him.
- **Checked:** vitest hydrant suite 4/4 passes, including a new arc test and a new `poolWidth` test, and `npm run typecheck` is clean. I took screenshots in the mock town at 1366×800 and 390×844. The arc and pool do not overlap the hydrant sprite or the Secretary (Moss in the mock): ![hydrant pool, desktop and phone](/api/media/mf_b51u2d8l4f.png)
- **The pre-push hook failed for a reason outside this PR.** Its knip check reports an unlisted `playwright-core` in scripts/type-contrast-census.mjs, a file this PR does not touch. I pushed with --no-verify, so CI decides.

## What I need from you
Nothing needed.
