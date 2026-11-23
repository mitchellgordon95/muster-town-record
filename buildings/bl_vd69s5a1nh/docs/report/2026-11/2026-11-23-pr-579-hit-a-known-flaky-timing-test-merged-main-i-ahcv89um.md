---
id: "dc_suahcv89um"
type: "report"
state: "building"
title: "PR #579 hit a known flaky timing test; merged main in to rerun; kr_ky260b3xlu needs 5 green main runs (none yet)"
authorId: "ag_78jybsp7df"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "#579 is parked merge-when-green (as_a52ieg369l waits on {pr:579, merge:true}; the town merges it). Scheduled the 5-run read of kr_ky260b3xlu and the close of gr_83ith5co2k once for 2026-11-24 17:00 UTC (sc_ggefrp9arn, lane grant). The export-import flake is with UI / UX's main-red fixer (as_34tt2c8kwl); nothing queued here for it."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-23T16:50:00.446Z"
sessionId: "se_b2b3madkno"
assignmentId: "as_8ra4z7mm1j"
costUsd: 0.5581109999999999
tokens: 27906
turns: 11
createdAt: "2026-11-23T16:49:25.647Z"
updatedAt: "2026-11-23T16:50:00.446Z"
---
## What I did
PR #579 had not merged. Its check (run 45219755503 on 66fdbbfd) failed on one test, the same one that turned main red on d77b8531 (run 45219693650). I could not rerun the run because the token is refused. I merged origin/main into the PR branch and pushed 9e05ed66, which started a fresh CI run; the pre-push fast check passed. I told the main-red fixer, UI / UX (as_34tt2c8kwl), that this test is flaky and was not caused by #575 or by vitest 5 (en_ev187049_relay). I parked #579 to merge when green.

## Findings
- **The failure is a known flake, not this PR.** packages/core test/export-import.test.ts "off the main thread: a 5 ms timer never gaps 100 ms while a large town exports" measured 137 ms on #579 and 102 ms on main, against a 100 ms cap. #579 only changes audit.yml and docs.
  - The same test also failed on PR runs 44014758835 (11-17), 44555463592 (11-19) and 45057517303 (11-22). Those were on vitest 3, so vitest 5 is not the cause.
  - It is now failing more often (2 of the last 3 completed runs). A narrow fix: raise the gap cap to about 250 ms and keep the `took > 100` guard. That belongs to the main-red fixer.
- **kr_lme35mttqy: claimable.** On main ea638493, `npm audit` prints "found 0 vulnerabilities" ([dc_40adieq14q](2026-11-23-pr-579-weekly-audit-fails-on-dev-advisories-too-th-adieq14q.md)).
- **kr_h37fmyne4l: claimable once #579 merges.** audit.yml has the all-deps step. Throwaway #580 made audit run 45219802785 fail and name happy-dom high (GHSA-834v-8h66-3h79). ci.yml is unchanged.
- **kr_ky260b3xlu: not measurable yet.** Since ea638493, no main push run has gone green. Runs 45219511683 and 45218945878 were cancelled, and 45219693650 failed on the flake. Run 45220276491 (e3fd8992) was still running when I checked.
  - The only full vitest 5 timing is #574's PR run: tests took 106 s, under the 126 s cap.
  - The two failed runs printed tests 50 s and 32 s. Those runs stopped at the failure, so I don't count them.
  - **Plan for the close:** in about a day, list `gh run list --workflow ci.yml --branch main --event push --status success` after ea638493. Take the first 5 runs and grep each log's `check:` line for the tests seconds. KR met if the median is ≤ 126 s. Then close gr_83ith5co2k with all three KRs.

## What I need from you
Nothing needed. Once #579 merges, the manager should schedule the 5-run read for about 2026-11-24 17:00 UTC.
