---
id: "dc_zhaf970f6m"
type: "report"
state: "building"
title: "gr_83ith5co2k done: vitest 5 tests median 100 s over 5 green main runs, audit 0, weekly audit covers dev deps"
authorId: "ag_i6t0q5ie27"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Closing gr_83ith5co2k on this evidence: 5 green main runs after ea638493 with tests median 100 s (cap 126 s), npm audit 0 on 0c51d5a3, audit.yml step 2 covers dev deps and failed on the throwaway happy-dom pin (PR #580)."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-24T17:01:42.818Z"
sessionId: "se_6a8kjwdm2v"
assignmentId: "as_kvfh6xv1v9"
costUsd: 0.9798870000000001
tokens: 48994
turns: 13
createdAt: "2026-11-24T17:01:25.036Z"
updatedAt: "2026-11-24T17:01:42.818Z"
---
## What I did
I confirmed PR #579 merged. I read the `check:` timing lines from the first 5 green main push runs after ea638493 and re-ran `npm audit` on today's main (0c51d5a3). I also checked audit.yml and the throwaway run. Topic page "Dependency advisories" ([dc_o70qzef90k](../../wiki/2026-10/2026-10-31-dependency-advisories-0qzef90k.md)) is rewritten.

## Findings
- **PR #579** merged 2026-11-23 16:54:55Z as b01da86a.
- **kr_ky260b3xlu (tests ≤ 126 s on vitest 5): met on the numbers.** These are the first 5 green `ci.yml` main push runs whose commit contains ea638493 (checked with `git merge-base --is-ancestor`). Tests seconds per run:
  - 45220276491 (e3fd8992): 80 s
  - 45220726452 (86f24796): 113 s
  - 45222032270 (00fa8521): 113 s
  - 45223009301 (6347f2a5): 100 s
  - 45224933121 (34ef090f): 82 s

  **Median 100 s** (range 80–113). The cap is 126 s and the vitest 3 baseline is 105 s. Total median is 124 s (100–145). Two later runs: ab02db89 at 103 s and 0c51d5a3 at 122 s.
- **kr_lme35mttqy:** `npm audit` on main 0c51d5a3 prints "found 0 vulnerabilities". The lock has vitest 5.1.1, happy-dom 21.0.4 and hono 4.13.21. Before #574 it reported 9 advisories: 2 critical, 1 high and 6 moderate.
- **kr_h37fmyne4l:** audit.yml on main has step 2, "audit all dependencies, dev included" (`npm audit --audit-level=high`, `if: !cancelled()`). ci.yml is unchanged. Throwaway PR #580 (CLOSED) pinned happy-dom 20.14.6. In its audit run 45219802785 the prod step passed and the all-deps step failed, naming happy-dom high (GHSA-834v-8h66-3h79).
- **Export-import flake:** it fired once after ea638493, in main run 45219693650 on d77b8531 ("expected 102.04 to be less than 100"). That run is red, so it is not one of the 5 green runs. UI / UX's fix (as_34tt2c8kwl) landed as PR #583 (00fa8521, branch agent/teo-1/…, merged 2026-11-23 16:56:00Z) and raised the cap to 250 ms. All runs since show the 250 ms test passing, so no cap fix is still owed.

## What I need from you
Close gr_83ith5co2k.
