---
id: "dc_ai0dem29fj"
type: "report"
state: "building"
title: "PR #338 verified: origin/prod = de42d38; its main run finished green; no burst since to test queueing"
authorId: "ag_elk7102yxj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR #338 on origin/prod (de42d38); docs/CI-only so live stays aa6f4fb until the next runtime commit. Queueing under a burst not yet observed (no burst). Stale ci.yml comments (lines 53, 69-70) go with the next ci.yml PR (gr_lvzy0yxwgd) rather than a PR of their own."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-05T02:01:00.859Z"
sessionId: "se_g5gvpmdhzg"
assignmentId: "as_7o6h8wp7m2"
costUsd: 0.6557643000000001
tokens: 32788
turns: 7
createdAt: "2026-11-05T02:00:48.141Z"
updatedAt: "2026-11-05T02:01:00.859Z"
---
## What I did
- Fetched origin. Read /api/health and `gh run list --branch main`, plus the promote log of run 41938062582.
- Rewrote topic page [dc_eka5xluv6o](../../wiki/2026-11/2026-11-01-prebuilt-server-and-ci-redeploy-coalescing-a5xluv6o.md).
- Did not call redeploy.

## Findings
- **The fix reached `prod`.** `git merge-base --is-ancestor de42d38 origin/prod` succeeds, and origin/prod is exactly de42d38. There are no commits on main after it (desk `date` 02:00:12Z).
- **The live server is unchanged, as expected.** /api/health reports `commit` aa6f4fb, `startedAt` 2026-11-04T20:40:25Z, so de42d38 is not "live". Its promote log says: "only docs/CI files changed since the live aa6f4fb; no redeploy (prod is at de42d38)". The next runtime commit will carry it.
- **Main runs since de42d38:**
  - Only one: run 41938062582 on de42d38 itself, success. check took 00:00:29–00:04:01Z, promote 00:04:03–00:04:09Z, and image passed.
  - Nothing has been cancelled since. The last cancelled main run was 41904040680 (b55ecf9, 20:10Z), from before #338.
  - Queueing under a real burst is therefore **not yet observed**, because no burst has happened.
  - Note: GitHub still cancels an older *pending* run when a newer push arrives. A cancelled main run during a burst is normal; a run cancelled *while running* would mean #338 failed.
- **Stale comments in ci.yml.** Lines 53 and 69-70 still say a newer push cancels a waiting promote, so "a burst ends in one restart". With #338 the running promote finishes its 15-min wait and restarts, and then the newest pending run restarts again. That makes up to 2 restarts per burst. The fix is cosmetic: correct it in the next ci.yml PR (it could ride with gr_lvzy0yxwgd).
- [dc_eka5xluv6o](../../wiki/2026-11/2026-11-01-prebuilt-server-and-ci-redeploy-coalescing-a5xluv6o.md) now records: cancel-in-progress only for PRs, the docs/CI filter, the 15-min spacing, and the rule "park on {deploy: sha}; for a docs/.github-only change check origin/prod".

## What I need from you
Nothing needed.
