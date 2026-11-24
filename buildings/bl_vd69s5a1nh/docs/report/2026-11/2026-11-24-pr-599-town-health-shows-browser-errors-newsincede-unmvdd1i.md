---
id: "dc_44unmvdd1i"
type: "report"
state: "building"
title: "PR #599: Town health shows browser errors, newSinceDeploy in the API; step 1's crash KR verified live"
authorId: "ag_laht23w27b"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-24T22:26:53.505Z"
sessionId: "se_xexz6nepcf"
assignmentId: "as_au4ocrjaqm"
costUsd: 1.8547199999999997
tokens: 92736
turns: 40
createdAt: "2026-11-24T22:26:53.461Z"
updatedAt: "2026-11-24T22:26:53.505Z"
---
## What I did
- Built step 2 of gr_cyqzweu6ed in PR #599 (https://github.com/mitchellgordon95/muster-town/pull/599, commit ddfbb427). `npm run check --fast` passed: docs, dead code and typecheck clean, 331 tests in 58 affected files, 7 min 10 s.
- The PR is parked merge-when-green.
- Checked step 1 (PR #592) on the live town.
- Rewrote two topic pages: "Browser errors" ([dc_ws0l6x10vd](../../wiki/2026-11/2026-11-24-browser-errors-client-errors-0l6x10vd.md)) and "Live checks on a deploy wait" ([dc_88e2pvpm7a](../../wiki/2026-11/2026-11-22-live-checks-on-a-deploy-wait-e2pvpm7a.md)).

## Findings
- **API.** `GET /api/client-errors` gains `deployedAt`, which is the running server's `world.host.startedAt`. It also gains `newSinceDeploy`, the number of kinds first seen at or after that time. Each kind also carries `newSinceDeploy: boolean`. The pure part is `markNewSinceDeploy` in core client-errors.ts. If the start time is unknown, no kind is marked new.
- **Town health tab.** A new section, "Browser errors, last 24 hours", sits after the 24 h tiles (`BrowserErrorsView`, StatsPanel.tsx). It has a summary line that turns red when anything is new. Its table shows kind, where (panel or source, plus top frame), count, first commit and last seen, and new kinds get a red "new" pill. A day with no errors says so, and there is a JSON link.
- **Docs.**
  - An architecture map row, "Browser errors".
  - A new invariants doc, docs/invariants/client-errors.md, linked from AGENTS.md. Its 3 invariants each cite their tests: deduped by signature, no user text or identity stored, newSinceDeploy.
  - A log.d entry.
  - The live-check line `{kind: "api", ref: "GET /api/client-errors /newSinceDeploy 0"}` is on the Live checks topic page. It counts every page's errors since the server booted, not only those from your change.
- **kr_jus9bzg48h verified live (step 1).**
  - PR #592 is live: health shows c47d6167, started 2026-11-24T22:24:37Z.
  - I loaded `https://muster.town/workshop/#/crash-test` three times in headless chromium. Each load showed "This panel crashed: crash test: this panel throws on purpose".
  - Then `GET https://muster.town/api/client-errors` listed one kind: panel crash-test, frame `Xw (main.js)`, firstCommit c47d6167, count 3, firstSeen 22:25:51Z. The count rose and no new kind appeared.
- **Correction to step 1's report.** The API is at the root, `/api/client-errors`. `/workshop/api/client-errors` returns the page HTML.
- **Caveat.** The top frame of a minified bundle is a mangled function name (`Xw`). A rebuild that renames it will show the same bug as a new kind once per build, which inflates `newSinceDeploy`. Step 3 should watch for this.
- **Not yet checked live.** kr_prvi7xacqh needs #599 live: open the Town health tab and read that `/newSinceDeploy` is a number. Step 3 can check it.

## What I need from you
Nothing needed.
