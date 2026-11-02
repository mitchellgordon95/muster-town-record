---
id: "dc_gq34e2h7ys"
type: "report"
state: "building"
title: "CI check job writes the per-step timing line to the job summary (PR #76 merged, a292c1a); PR #71 closed"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["mt_xywhisvdcm","dc_tt1fskf9mq"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/76","https://github.com/mitchellgordon95/muster-town/actions/runs/40905322139"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: PR #76 merged (a292c1a), timing line in the CI job summary, PR #71 closed. Folded into the next rollup that has something bigger (Mitchell can open run 40905322139 to see the summary)."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-29T15:51:41.302Z"
sessionId: "se_hhmaguf2w0"
assignmentId: "as_39vz8ntpax"
costUsd: 0.6470534000000001
tokens: 32353
turns: 14
createdAt: "2026-10-29T15:51:25.498Z"
updatedAt: "2026-10-29T15:51:41.302Z"
---
## What I did
- Changed `.github/workflows/ci.yml` (PR #76, https://github.com/mitchellgordon95/muster-town/pull/76, merged as a292c1a). The check step now runs `npm run check 2>&1 | tee check.log` with `shell: bash`, which turns on pipefail, so a red check still fails the job. A new step after it runs on every run that isn't cancelled, red ones included. It copies the last `check: … total …` line into `$GITHUB_STEP_SUMMARY`. If the check stopped before printing a timing line, it writes a fallback line saying so instead.
- Closed draft PR #71 (the pre-push hook) with a comment pointing to the Town Hall decision.

## Findings
- PR run 40904958399 and main run 40905322139 (a292c1a) both passed on the first attempt. Every step was green, including the new summary step. The line that step copies, from main: `check: docs 0s | deadcode 4s | typecheck 16s | tests 1m20s | total 1m41s`.
- I tested the summary step's shell locally on two inputs. On a failed check it writes `` `check: docs 1s | total 3s | FAILED at docs` ``. On an empty log it writes the fallback line.
- Not checked: the summary itself on the run page. GitHub's API doesn't return job summaries. What I did confirm is that the step succeeded and its grep pattern matches the line in the log. Open run 40905322139 on GitHub to see it.
- No redeploy needed: only the CI workflow changed. The timings-history doc gets re-proposed only if a slowdown shows up.

## What I need from you
Nothing needed.
