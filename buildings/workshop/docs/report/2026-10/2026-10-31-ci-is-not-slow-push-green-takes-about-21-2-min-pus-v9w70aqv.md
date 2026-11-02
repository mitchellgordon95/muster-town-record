---
id: "dc_mvv9w70aqv"
type: "report"
state: "building"
title: "CI is not slow: push → green takes about 2½ min, push to main → live about 3 min; forks should park 5 min on CI, not 12-30"
authorId: "ag_8bo7q9za38"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Measured: push → green 2.4 min median / 2.8 p90, push to main → live 2.7 min median; CI row 5 on Town blockers; habit page now 5 min parking. as_7a33e2woff ({pr: N} wait) replaces the guess altogether. Told Mitchell in mt_3jtclcoxl2."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T20:30:22.763Z"
sessionId: "se_om0i6t8fvx"
assignmentId: "as_8yyuh71kr7"
costUsd: 1.2594498
tokens: 62972
turns: 32
createdAt: "2026-10-31T20:29:59.420Z"
updatedAt: "2026-10-31T20:30:22.763Z"
---
## What I did
I pulled the last 200 runs of `.github/workflows/ci.yml` (the last ~44 hours, ending a few minutes before this report) and their job and step timings from the GitHub API. I read the `npm run check` timing line from the logs of 60 green runs. I matched each green push to main to the event log's "Redeploy finished … at <sha>" line to measure how long until it was live. I didn't change CI. No PR.

## Findings
All durations are in plain minutes.
- **Runs:** 200 in total: 164 green (95 PR, 69 main), 14 red, 22 cancelled (a newer push to the same branch replaced them).
- **Queue wait** (a runner picks the job up): median **0 min**, max 0.2 min. GitHub never made us wait.
- **Push → green:** median **2.4 min**, p90 **2.8 min**, max 3.8 min. PRs: 2.3 / 2.6 min. Main: 2.5 / 3.0 min.
- **Main green → live:** median 0.1 min, p90 1.5 min, max 2.2 min.
- **Push to main → live:** median **2.7 min**, p90 **4.3 min**, max 5.8 min (all 69 green main pushes matched).
- **The slowest step is the tests.** Inside the ~2 min `npm run check` (median 122 s): tests take 99 s (p90 108 s), typecheck 18 s, knip 4 s, docs 0 s. `npm ci` takes 6 s because the npm cache is already on, and the web build takes 6 s. In one run split by package: core 29 s, server 13 s, runtime 12 s, web 6 s, cli 5 s, desk 1 s. The packages run one after another.
- **Cache or split:** a cache wouldn't help, since npm is already cached and the build is 6 s. Running the six test suites in parallel, or as a matrix job, would save at most ~1 min of the 2.4. I don't think it's worth doing.
- **What actually makes CI feel slow:** forks park 12-30 min waiting on a run that takes 2½. Every fork that parks on CI should drop its window to **5 min** (re-park 5 min in the rare case it's still running). That covers the PR-merge continuations like Pix 1's map-shape rescue (as_l8lpo5lbiy, parked ~30 min) and Pix 2's step-2 rescue (as_1apdltfxu1). I changed the CI-parking line on "Live checks and dev habits" ([dc_cvnjh0v7mj](../../wiki/2026-10/2026-10-28-live-checks-and-dev-habits-njh0v7mj.md)) from +10 min to +5 min. Whoever writes "resumes in N min" into a continuation (the team lead) should use 5.
- **Town blockers page** ([dc_nhd0maw3f5](../../wiki/2026-10/2026-10-28-town-blockers-d0maw3f5.md)): I added row 5, "CI run time, push → green: 2.4 min median / 2.8 min p90 / 3.8 min max, last 44 h, 164 green runs", plus a section with the numbers above.

## What I need from you
Nothing needed.
