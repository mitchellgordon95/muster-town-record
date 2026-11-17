---
id: "dc_f1ex6z35gm"
type: "report"
state: "building"
title: "1:1 fix f83b8f50 is live; live screenshot needs a human-opened 1:1"
authorId: "ag_wmmis99kvr"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: the request is done."
decidedBy: "system"
decidedAt: "2026-11-17T18:27:21.288Z"
sessionId: "se_jluni0o8yn"
assignmentId: "as_x3chcwb2b5"
costUsd: 0.728324
tokens: 36416
turns: 18
createdAt: "2026-11-17T18:27:21.279Z"
updatedAt: "2026-11-17T18:27:21.288Z"
---
## What I did
- Checked that the fix is live, then looked for a 1:1 I could watch or open.
- Rewrote the topic page [dc_pm3sxczr6d](../../wiki/2026-11/2026-11-17-1-1-live-progress-writing-line-and-tool-calls-3sxczr6d.md), including how to test on live.

## Findings
- **The fix is live.** Live /api/health shows commit d863e456, started at 18:26:02Z. That commit contains f83b8f50 from PR #492.
- **No 1:1 is live right now.** In GET /api/meetings, every one-on-one is done. The most recent was Mitchell's 1:1 with the Secretary, mt_vdu3iqhasi, opened at 18:04Z. That was before the deploy, so it ran the old code.
- **I can't open a 1:1 myself.** createOneOnOne (core/meetings.ts:182) accepts only a human with direct rights. The test account holds role:visitor only, with no access request. Its POST /api/buildings/bl_t7slw19vgg/one-on-one returned 403 "Ask for access first". Its roles did not change.
- **A past 1:1 can't be checked afterwards.** The drafting marks are kept in memory only. They are not events.
- **This chain can't park again.** It has parked 3 times in a row, so I'm closing it.
- **Still standing:** the before evidence (mf_6yu1kh2owv) and the after screenshots from a local real stack (mf_gmm90vgn1q, mf_r57c6c21x7), all from [dc_y42w3871ym](2026-11-17-1-1-is-writing-and-live-tool-calls-cause-found-fix-2w3871ym.md).
- **What Mitchell should see in his next 1:1 with a manager.** While the manager works, the panel shows "<Name> is writing…" and under it "▸ <Name>: N tool calls so far · <newest call>". This should hold even after the manager's "On it…" line. The writing line goes away when the manager posts its answer and goes idle.
- **How to check it live.** If a check on a live 1:1 is wanted, queue an assignment while a human has one open. The watcher /home/agent/tools/watch_1on1.py and the steps on [dc_pm3sxczr6d](../../wiki/2026-11/2026-11-17-1-1-live-progress-writing-line-and-tool-calls-3sxczr6d.md) cover it.

## What I need from you
Nothing needed.
