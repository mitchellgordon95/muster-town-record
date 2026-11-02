---
id: "dc_3f063fybel"
type: "report"
state: "building"
title: "Rollup cadence: \"something new is live and decided, ≥4 h apart\" merged (PR #164, 76a6065)"
authorId: "ag_pkg9ex6cpm"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_7mhv73quu3","dc_w6e1vpbkuf"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/164"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "76a6065 is live (prompt already shows the new cadence line). I'll update my private Rollup format page myself. Goes into rollup 35 as a Decided line."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T16:54:55.946Z"
sessionId: "se_z5m19mtyo5"
assignmentId: "as_65e14yg5lf"
costUsd: 1.0577458999999998
tokens: 52887
turns: 25
createdAt: "2026-10-31T16:51:58.831Z"
updatedAt: "2026-10-31T16:54:55.946Z"
---
## What I did
Replaced the 24 h rollup rule (town hall 10-25 decision 5) with Mitchell's rule from 1:1 mt_7mhv73quu3 decision 1. The change is in PR https://github.com/mitchellgordon95/muster-town/pull/164. CI passed and I merged it as **76a6065**. Main CI promotes merges by itself, so I didn't call `redeploy`: a manual redeploy right after a merge can rebuild the old prod ([dc_hucb0om4nz](2026-10-31-live-check-of-9253c18-parked-live-is-2968f42-main-cb0om4nz.md)). **76a6065 should be live** once that promotion finishes. At 16:55Z the live server was still on fa73e88.

## Findings
- **`packages/core/src/prompts.ts`:**
  - `ROLLUP_RULE_HOURS = 24` is replaced by `ROLLUP_MIN_GAP_HOURS = 4`.
  - The rollup rule in `managerIntrayBlock` now reads: "Roll up when something new is live (a commit went live since your last rollup) and the reports that cover it are decided, or when a covered report hit an escalation criterion; keep at least 4 h since your last rollup (escalations excepted) so a run of small PRs lands as one item; nothing happened → no rollup."
  - The block has a new line built from `world.host.commit` and `world.host.startedAt`, for example "Live: fa73e88 since 07:12Z 2026-10-31, 4h ago (newer than your last rollup)". The ending is "(already live at your last rollup)" or "(no rollup yet)" in those cases, and "Live: unknown (no runtime)" when there is no runtime.
  - In `managePrompt`, "One rollup per day, or sooner on escalation" became "Roll up when something new is live and decided (at least 4 h apart), or sooner on escalation".
- **Limitation:** `startedAt` is when the server started, so a restart with no new code also counts as "newer than your last rollup". The manager still checks the sha.
- **Docs:** `docs/waterfall.md` §3.1 (rule of thumb) and §3.2 "When" now use the same wording and cite the 1:1. I added a line to `docs/log.md`. No other copies of the 24 h rule turned up in AGENTS.md, CLAUDE.md, docs/*.md or the web code.
- **Tests:** I updated the `prompts.test.ts` assertion and added a test for the new rule text and the three states of the Live line. `prompts.test.ts`, `rollup-format.test.ts` and `flags.test.ts` pass (21/21), `npm run typecheck` is clean, and CI is green.
- **Topic pages:**
  - "Workshop standing rules" ([dc_w6e1vpbkuf](../../wiki/2026-10/2026-10-28-workshop-standing-rules-e1vpbkuf.md)) has a new Rollup cadence line.
  - "Live checks and dev habits" ([dc_cvnjh0v7mj](../../wiki/2026-10/2026-10-28-live-checks-and-dev-habits-njh0v7mj.md)) never mentioned the cadence, so I left it as is.
  - I didn't touch Pix's private "Rollup format" page (dc_nntzjwwdea). Pix should update its cadence wording to match.

## What I need from you
Nothing needed.
