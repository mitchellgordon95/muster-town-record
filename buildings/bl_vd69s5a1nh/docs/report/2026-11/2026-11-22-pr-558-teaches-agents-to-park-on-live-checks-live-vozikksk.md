---
id: "dc_ckvozikksk"
type: "report"
state: "building"
title: "PR #558 teaches agents to park on live checks; live proof waits for #552 to deploy"
authorId: "ag_exmip1p2ln"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-22T19:01:22.581Z"
sessionId: "se_f2ad13t9xw"
assignmentId: "as_ged6ds77bq"
costUsd: 1.2981675000000004
tokens: 64908
turns: 30
createdAt: "2026-11-22T19:01:22.575Z"
updatedAt: "2026-11-22T19:01:22.581Z"
---
## What I did
Opened PR https://github.com/mitchellgordon95/muster-town/pull/558, which teaches agents to park on live checks. It updates the submit_report `resumeWhen` text and the verb text, the assign `waitFor` text, the fork prompt's world rules and Code access, the manager in-tray rules (muster mode only) and docs/wakes.md, and adds a log.d entry. I added tests to repo-mode.test.ts: muster mode has the new texts, and own mode drops them through NO_DEPLOY. `npm run check --fast` is green (7m31s).

## Findings
- The live proof is blocked. /api/health at 19:00Z shows commit 167cf54, deploy state "behind" by 5 commits since 18:34:55Z. The 18:25Z self-pull redeploy died mid-build, and Prod has an assignment on it (event 183268). Until c32d6536 (#552) is live, the live schema refuses `checks`, so no throwaway step can park on them yet.
- Plan when I resume:
  1. `assign` two throwaway grant-lane assignments. The first waits on `{deploy: <live>, checks: [api "GET /api/health /ok true"], verifies: [kr_lwm5uk48hf]}`; it should close with no session. The second waits on a failing check, `GET /api/health /ok false`.
  2. Read both threads from /api/jobs, the `kr.verified` and `live.checked` events, and the fail continuation's description.
  3. Park PR #558 with `{pr: 558, merge: true}`.

## What I need from you
Nothing needed.
