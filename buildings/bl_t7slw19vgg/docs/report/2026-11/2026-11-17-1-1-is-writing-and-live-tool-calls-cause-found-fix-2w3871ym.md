---
id: "dc_y42w3871ym"
type: "report"
state: "building"
title: "1:1 \"is writing…\" and live tool calls: cause found, fix in PR #492, parked on CI"
authorId: "ag_honhuk6iyt"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-17T04:06:10.730Z"
sessionId: "se_1q7bzppdbg"
assignmentId: "as_eym5iqtca7"
costUsd: 3.0087086999999997
tokens: 150435
turns: 74
createdAt: "2026-11-17T04:06:10.725Z"
updatedAt: "2026-11-17T04:06:10.730Z"
---
## What I did
- Reproduced the bug on live while Mitchell's 1:1 with Pix (mt_5rznhkoi6r) was open. I polled `/drafting` and Pix's events every 4 s, and took headless screenshots of the meeting panel as a guest.
- Found the cause, fixed it and wrote a runtime test. The test fails before the fix and passes after.
- Proved the fix on a local real server and runtime, with a scripted manager.
- Opened PR #492: https://github.com/mitchellgordon95/muster-town/pull/492
- Wrote the topic page [dc_pm3sxczr6d](../../wiki/2026-11/2026-11-17-1-1-live-progress-writing-line-and-tool-calls-3sxczr6d.md).

## Findings
- **What Mitchell sees now (live 7a886f88).**
  - The text is "<Name> is writing…". Under it is a folded line, "▸ <Name>: N tool calls so far".
  - Both show only while the agent is on the server's drafting list.
  - In Pix's 1:1, 119 polls over about 9 min returned an empty drafting list 117 times. Pix was running Read, Grep and Glob the whole time.
  - The 2 non-empty polls came right after Pix called `meeting` listen. That is the "sometimes".
  - Before screenshot: /api/media/mf_6yu1kh2owv.png. Pix's "On it" line is there and Pix is still working, but nothing shows under it.
- **Cause.**
  - Only the meeting verb's `listen` and `status` set the drafting mark (core/meetings.ts).
  - A manager answers a 1:1 from lines the runtime pushes straight into its session (runtime/manage.ts), so it rarely calls `listen`.
  - Its "On it…" line also clears the mark while the work goes on.
  - The client's events feed was not the problem: it is not filtered and holds 600 events, about 14 min.
  - The timestamps were not the problem either.
- **Fix (PR #492).**
  - The runtime marks the manager as drafting when it feeds the 1:1's prompt or a human's line.
  - It also marks it on each non-meeting tool call of a manage session while that manager has a live 1:1. Each mark restarts the 5 min window.
  - It clears the mark when the turn ends with nothing queued.
  - The live fold now names the newest call next to the count, on one line.
  - Docs updated: docs/meetings.md §7 and docs/log.d.
- **After screenshots (local real stack).**
  - /api/media/mf_gmm90vgn1q.png: "Mei is writing…" and "▸ Mei: 5 tool calls so far · Reading GoalTreePanel.tsx" after "On it."
  - /api/media/mf_r57c6c21x7.png: the answer posted with "▸ 6 tool calls", and the writing line gone.
- **Checks.**
  - Typecheck is green, and the related core and runtime tests pass (35 tests, plus 11 in one-on-one).
  - `check --fast` fails at deadcode on `playwright-core` in scripts/type-contrast-census.mjs. It fails the same way on main, so it is not from this PR.
- **Test account.** It holds role:visitor only, with no join request, so it cannot open a 1:1. I didn't change it and no reset was needed.
- **Live status.** Nothing is live yet. Once the PR merges, its squash commit should go live through CI. The town FYI says CI deploys were broken earlier, but live is now at 7a886f88, two commits behind main.

## What I need from you
Nothing needed.
