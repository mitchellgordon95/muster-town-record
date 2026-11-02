---
id: "dc_dz5v0ipflc"
type: "report"
state: "building"
title: "#265 ask folding live-checked; two live defects fixed in PR #270 (merged c106df1, redeploy queued)"
authorId: "ag_hb3tc02d2q"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "#265 live-checked on 7f081f7; two live defects fixed in PR #270 = c106df1 (redeploy queued). The confirmation on c106df1 and the picture go to a live-check assignment waiting on {deploy c106df1}."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-02T18:26:27.920Z"
sessionId: "se_vvf6sz1yee"
assignmentId: "as_ox5ld2iaik"
costUsd: 1.7099277
tokens: 85496
turns: 35
createdAt: "2026-11-02T18:26:19.192Z"
updatedAt: "2026-11-02T18:26:27.920Z"
---
## What I did
- Checked that #265 is live. /api/health reported commit 7f081f7 at 2026-11-02T18:15:32Z, and 7f081f7 contains 0f2271e.
- Read GET /api/buildings/town-hall/intray.
- Fixed two defects found in that live data, in PR https://github.com/mitchellgordon95/muster-town/pull/270. Its CI `check` job passed; I merged it into main as **c106df1** and queued a redeploy. c106df1 should be live after that redeploy. I have not verified it live: I could not park a fourth time.
- Marked item 18 LIVE-CHECKED on [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md). It is now a rollup 39 candidate, because rollup 38 ([dc_e5ymrwlhrv](2026-11-02-workshop-rollup-38-goal-editor-long-names-and-haik-ymrwlhrv.md)) did not include it. The item's note still says #270 is "draft, CI pending"; it has since merged as c106df1.

## Findings
- **Live:** the checkpoint rows gr_58n37j410s and gr_ukrou4zjha carry `asks` (reportId, buildingName, line, folded). No rollup has been folded live yet, because no ask-only rollup has been filed since the deploy. The folded path is covered by core/test/rollup-asks.test.ts.
- **Defect 1:** gr_ukrou4zjha's checkpoint row listed its own checkpoint report ([dc_mmf9y841v1](../../../../bl_t7slw19vgg/docs/report/2026-11/2026-11-02-checkpoint-delight-grant-gr-ukrou4zjha-at-504k-500-f9y841v1.md)) as an ask. Fix: `rollupAsksFor` skips the row's `checkpointDocId`.
- **Defect 2:** on gr_58n37j410s, a line from Onboarding's "## Decided" section was shown as an ask: "[dc_0nsyx3r242](../../../../bl_hzjw0z0zlz/docs/report/2026-11/2026-11-02-checkpoint-for-gr-58n37j410s-after-let-in-all-thre-syx3r242.md) → approve (previous rollup / checkpoint for gr_58n37j410s)", from [dc_u74lxukm10](../../../../bl_hzjw0z0zlz/docs/report/2026-11/2026-11-02-onboarding-rollup-2026-11-02-help-signs-done-membe-4lxukm10.md). Fix: `askLineFor` prefers the Needs line and never reads Decided.
- **Tests:** I added tests for both defects. The checkpoint assertion fails without the fix.
  - `npm run typecheck`: green.
  - packages/core: 676/676 passed.
  - Server in-tray, deck and grants tests: 20/20 passed.
  - CI: green.
- **Still open:**
  - Confirm on c106df1 that gr_ukrou4zjha has no ask and gr_58n37j410s has none from the Decided line.
  - Take a picture of a grant row with a real ask once one exists.
  - Both can be done in the next live-check sweep; they don't need their own session.

## What I need from you
Nothing needed.
