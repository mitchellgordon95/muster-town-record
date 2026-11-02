---
id: "dc_hw7h25fyn7"
type: "report"
state: "building"
title: "Close grant button enabled without a note: PR #165 merged (49fb455), parked on its deploy"
authorId: "ag_ytbm4a43so"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_kdsxeqo6ot"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/165"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #165 (49fb455) merged; the live check is already parked as as_3i5f70ys2v waiting on deploy 49fb455, so no new assignment. Goes into rollup 35 as a Shipped item (Mitchell's ask from 1:1 mt_kdsxeqo6ot) once 49fb455 is live and the live check is decided."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T17:32:17.150Z"
sessionId: "se_4mi1q8evmj"
assignmentId: "as_h8arrmelsd"
costUsd: 0.6015608
tokens: 30078
turns: 17
createdAt: "2026-10-31T17:32:07.653Z"
updatedAt: "2026-10-31T17:32:17.150Z"
---
## What I did
Made "Close grant" clickable with an empty note, as Mitchell asked in 1:1 mt_kdsxeqo6ot. PR https://github.com/mitchellgordon95/muster-town/pull/165: CI green, merged to main as **49fb455**. Main CI promotes it to prod. I did not run a manual redeploy because one right after a merge rebuilds the old build ([dc_hucb0om4nz](2026-10-31-live-check-of-9253c18-parked-live-is-2968f42-main-cb0om4nz.md)). Live was still 76a6065 when I submitted this.

## Findings
- **Web** (`packages/web/src/panels/Places.tsx` GrantRow): the `disabled={!note.trim()}` check is gone. The Note placeholder now reads "optional: the evidence the work is done".
- **Server** (`core/src/grants.ts` `closeDone`): `CloseGrantInput.note` already defaulted to "", but `closeDone` refused a blank note. Now a human who leaves it blank gets the note "Closed as done by <name> from the Town Hall." It goes on the key result's claimed note and on the grant's history line, so neither is ever blank. The funders' notice now names the human instead of "The manager". The manager agent's `close_grant` still has to give evidence.
- **Mock sim** (`mock/sim.ts closeGrant`) uses the same default.
- **Test**: a new case in `core/test/lanes.test.ts` checks that a manager's blank note is refused, and that a human's blank close is accepted with the default note on the key result and the history line. Typecheck passes; the core lanes tests (23), server grants tests and web tests (189) all pass.
- I didn't touch gr_iq5m7dug56 or gr_tvt32g9xly.
- **Next session**: once 49fb455 is live, check the row signed in if a funded grant exists. Otherwise do a code read and crop the row.

## What I need from you
Nothing needed.
