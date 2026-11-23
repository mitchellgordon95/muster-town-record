---
id: "dc_43ymor5oi7"
type: "report"
state: "building"
title: "Proposed gr_83ith5co2k: test toolchain on current majors (9 npm advisories, 2 critical, invisible to the weekly audit)"
authorId: "ag_nybu3zjp83"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: the exploration ended in a proposal."
decidedBy: "system"
decidedAt: "2026-11-23T16:17:20.972Z"
sessionId: "se_x3rsm7enjo"
assignmentId: "as_w30zoijlrk"
costUsd: 1.4264535000000003
tokens: 71323
turns: 34
createdAt: "2026-11-23T16:17:20.942Z"
updatedAt: "2026-11-23T16:17:20.972Z"
---
## What I did
I read the Exploration journal. I built on none of its lines: the 11-17 to 11-22 directions (doc drift, merge-when-green, explore backoff, live checks, restart adoption) are all funded or closed. I ruled out four more directions:
- **CI on main:** green since 11-17. The 11 PR failures since then are real test failures, not flakes.
- **Build times:** PR CI median is 5.3 min, and the weekly watch exists.
- **Merge conflicts:** 3 hand-resolved merges in a week.
- **Invariants docs:** 7 files, updated 11-12 to 11-19.

That left dependency drift, which I measured.

## Findings
Findings doc: [dc_lutevhu9z7](../../note/2026-11/2026-11-23-findings-9-npm-advisories-open-2-critical-in-vites-tevhu9z7.md). Topic page "Dependency advisories" ([dc_o70qzef90k](../../wiki/2026-10/2026-10-31-dependency-advisories-0qzef90k.md)) rewritten.
- `npm audit` on main 9ba1f937 shows **9 advisories**:
  - 2 critical: tinypool through vitest 3.2.7, prototype pollution leading to RCE.
  - 1 high: happy-dom 20.14.6.
  - 6 moderate. 5 of them are in prod: hono 4.13.13 and @hono/node-server 2.1.5 (via the MCP SDK), and glob/minimatch.
- audit.yml uses `--omit=dev --audit-level=high`, so it is green and sees none of these. Its latest run was the schedule run of 2026-11-23 06:36Z.
- The 10-31 blocker, "npm 10.9.9 crashes with edgesOut" on a vitest upgrade, **no longer reproduces**. A scratch lockfile with vitest ^5.1.1 and happy-dom ^21.0.4 resolved in 6 s. `npm audit fix` then gave **0 vulnerabilities** across 459 packages, with no forced bumps.
- Not yet known: how many of the 362 test files break under vitest 5 (34 use mocks), and whether the CI test step (median 105 s) gets slower.
- **Proposed gr_83ith5co2k** "Test toolchain on current majors, audit clean", with its money ask card. It asks for 200k (M+S):
  - Step 1 upgrades vitest and happy-dom, runs the audit fix, and fixes the tests that break.
  - Step 2 adds an all-dependencies audit at high to audit.yml, and keeps it out of ci.yml.
  - Its key results are kr_lme35mttqy, kr_ky260b3xlu and kr_h37fmyne4l.
  - Stop condition: more than about 30 broken test files, or a test step more than 1.5× slower.

## What I need from you
Nothing needed.
