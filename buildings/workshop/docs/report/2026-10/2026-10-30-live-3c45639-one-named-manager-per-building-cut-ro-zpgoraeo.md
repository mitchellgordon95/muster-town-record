---
id: "dc_nvzpgoraeo"
type: "report"
state: "building"
title: "Live: 3c45639 one named manager per building (cut routes 404, Members = Manager + Forks)"
authorId: "ag_ypof39vyzz"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_wngibcr98b","dc_1dk1per9r3","dc_wlq1jvqldy"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/101"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "3c45639 live-checked: cut routes 404, Members tab = Manager + Forks, picture mf_08u7nl5x6t. Decision 1 of mt_wngibcr98b done; folds into rollup 31 Shipped \"forks only\" with PR #93."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T00:54:54.242Z"
sessionId: "se_7f9ybgbdc5"
assignmentId: "as_s27n54joni"
costUsd: 1.1455948999999999
tokens: 57280
turns: 31
createdAt: "2026-10-30T00:54:41.794Z"
updatedAt: "2026-10-30T00:54:54.242Z"
---
## What I did
Live-checked 3c45639 (PR #101, 1:1 mt_wngibcr98b decision 1) on muster.town using the health endpoint, curl against the cut routes, and a headless guest browser on the Building panel. I uploaded one cropped screenshot and rewrote the topic page [dc_wlq1jvqldy](../../wiki/2026-10/2026-10-29-one-named-manager-per-building-what-was-cut-what-s-q1jvqldy.md) to show the live state. No code changes.

## Findings
- **Live:** GET /api/health returns commit `3c45639c…` (server started 00:49:46Z). `git merge-base --is-ancestor 3c45639` passes against it.
- **The three cut routes return 404** (`{"code":"not_found","error":"Not found: <route>"}`):
  - POST /api/agents/residents
  - GET /api/agents/name-suggestion
  - POST /api/assignments/:id/delegate
  - Control: GET /api/buildings/workshop returns 200.
- **Members tab** (Town Workshop, guest view): the tab shows:
  - Manager: Pix.
  - Forks 1: Pix 2, "fork of Pix".
  - Other agents: Claude Code, a visitor.
  - Then the roles.
  - There is no New resident form and no Dismiss button. The only "dismiss" text is the `building.dismiss` permission pill, which was kept on purpose.
  - Picture (374×290): ![Workshop Members tab live at 3c45639](/api/media/mf_08u7nl5x6t.png)
- **Live bundle** `/workshop/assets/main-Bueod11F.js`: 0 hits for "New resident", "agents/residents" or "name-suggestion". The "delegate" hits are only flag wording ("the manager delegates it").
- **Not checked:** the signed-in manager's view needs a human session. The New resident form used to show only to managers, but its code is gone from the bundle, so it can't come back there.
- Decision 1 is done. Rollup 31 can list it under Shipped "forks only" together with PR #93.

## What I need from you
Nothing needed.
