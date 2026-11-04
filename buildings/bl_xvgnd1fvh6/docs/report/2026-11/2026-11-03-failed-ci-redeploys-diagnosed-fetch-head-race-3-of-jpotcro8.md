---
id: "dc_shjpotcro8"
type: "report"
state: "building"
title: "Failed CI redeploys diagnosed (FETCH_HEAD race, 3 of 30 runs; main undeployed since 19:25Z) and fixed; redeploy-failed alert added: PR #285, waiting on CI"
authorId: "ag_2jb020qorm"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Diagnosis is solid (FETCH_HEAD race, 48/60 vs 0/60 reproduction). Note main is already live again (97a9570 since 22:21Z), so the \"undeployed\" state cleared on its own; the parked continuation as_nl1tptip01 (waiting on PR #285 CI) merges and verifies the fix. Folded into the next rollup."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-03T22:23:54.364Z"
sessionId: "se_ssl3gvmymk"
assignmentId: "as_7b3dqn9fon"
costUsd: 1.6799438000000004
tokens: 83997
turns: 38
createdAt: "2026-11-03T22:23:41.007Z"
updatedAt: "2026-11-03T22:23:54.364Z"
---
## What I did
Pulled the live event log for 11-02 to 11-03 and found the failed step's output. Reproduced the failure on my desk and fixed it. Added a `redeploy-failed` monitor metric with tests. Opened PR #285: https://github.com/mitchellgordon95/muster-town/pull/285 (it's ready for review; I'm waiting on CI).

## Findings
- **Why it failed:** event 102835 at 11-02 03:57:37Z shows git's own error: `fatal: Cannot rebase onto multiple branches.` (exit 128). The fetch itself worked (`024b236..92336d0 prod`), so this wasn't an auth or network problem.
- **It keeps happening:** the same error hit at 11-03 18:26:09Z (event 108222) and 19:25:10Z (event 108448). That's 3 failed runs out of 30 that ended between 11-02 03:04Z and now. **Main is undeployed right now:** live is ae3c410 and main is 97a9570 (PR #284 has waited since 19:25Z).
- **Cause:** a race between two git commands in the same checkout. Every 5 min, runtime `code.ts` runs `git fetch origin +refs/heads/main:…` for the manage-session code snapshot. That fetch rewrites FETCH_HEAD while the redeploy's `git pull --rebase origin prod` is reading it. The lock-file check in code.ts is check-then-act, so the two can still overlap.
  - Running both commands at once on git 2.39 (the prod image is bookworm), the pull failed 48 times out of 60.
  - With `--no-write-fetch-head` on the code fetch, it failed 0 times out of 60.
- **Fix (PR #285):** that one flag, added in `packages/runtime/src/code.ts`.
- **Alert (PR #285):** a new metric `redeploy-failed` in `packages/server/src/monitor.ts`. I used a kebab-case key like the other metrics, not `redeployFailed`.
  - It reads the latest redeploy event that ended its run (`payload.terminal`). It goes red straight away when that run ended `failed` or `aborted`.
  - The value is the number of minutes since the failure. The FYI title names the failed step and who requested the run.
  - It stays red while a later run is still in progress. It clears 5 samples after a run reaches `done`.
  - Red raises the usual alert event and Prod FYI and shows in `/api/health` `monitor.alerts`. Wright's pinger forwards any red key, so it texts Mitchell once.
  - I added a row to the deploy/README.md Monitoring table.
- **Tests:** two new tests in `test/monitor.test.ts` (32 pass): the thresholds test, and the probe reading terminal events from a real world. `code.test.ts` passes 4/4 and the root typecheck is green.
- **After the deploy:** once CI ships the merge, the latest run that ended will be `done`, so the metric should start green. Before this deploy, the old code can still race. If CI's redeploy of the merge itself fails, a manual redeploy from the Town Hall ships it.
- **Topic page:** "Monitor internals" ([dc_orhwzyxs59](../../wiki/2026-10/2026-10-29-monitor-internals-hwzyxs59.md)) is rewritten with this.

## What I need from you
Nothing needed. I'll merge PR #285 when CI is green.
