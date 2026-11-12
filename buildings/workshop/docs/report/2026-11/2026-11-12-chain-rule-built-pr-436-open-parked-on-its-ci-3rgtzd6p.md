---
id: "dc_gj3rgtzd6p"
type: "report"
state: "building"
title: "Chain rule built: PR #436 open, parked on its CI"
authorId: "ag_pxke9xzdit"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Step 1 of gr_2r17x8egrc is built on draft PR #436 and parked on its CI; the continuation as_5xnradwd1f (merge when green, park on the deploy, read the boot event as kr_ig32y08ihi's evidence) is already waiting on {pr: 436}. Nothing more to queue."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-12T16:41:28.285Z"
sessionId: "se_iv2pl1zah2"
assignmentId: "as_zf4kr77hai"
costUsd: 1.8558466999999998
tokens: 92792
turns: 41
createdAt: "2026-11-12T16:41:15.809Z"
updatedAt: "2026-11-12T16:41:28.285Z"
---
## What I did
Built the chain rule from [dc_q0838kcg6c](2026-11-12-chain-rule-stopped-before-code-ui-ux-already-sits-838kcg6c.md) with Mitchell's answer to ak_pzu7q469my ("Keep it under Steer"). I opened draft PR https://github.com/mitchellgordon95/muster-town/pull/436 and am parked on its CI.

## Findings
- **Core.** `Goals.chainConflict(goalId, exceptBuildingId?)` and `requireChainFree` are in packages/core/src/goals.ts. A lab at, above or under the goal blocks it. Labs only: the Town Hall is exempt. The root is shared, so a lab at the root sits on no chain. Without that, seeds and hosted collectives, whose labs start at the root, could never add a second building.
- **What is refused (409).** createBuilding refuses an occupied chain, and so does the v0 import, which goes through createBuilding. attach refuses it before the desk-total check. adoptGoal now also refuses a goal that has a lab under it.
- **Goal moves.** A move that a human makes or accepts is allowed even when it puts two labs on one chain. Its `goal.moved` event records the overlap in `chainOverlaps`.
- **Boot audit.** server main.ts appends one `system` event after the Secretary setup: "chain audit: N violations, M accepted exceptions: …". A pair of labs on one chain counts as accepted when a human moved a goal between them to where it is now.
- **Expected on muster.town.** I ran the audit logic against the live GET /api/goals tree and it finds exactly one pair: UI / UX under the Town Workshop. Its goal gl_bl_t7slw19vgg was moved under gl_join by us_1la74k332n (Mitchell) at 2026-10-31T04:16:54Z, so the boot event should read 0 violations and 1 accepted exception.
- **Tests run here.**
  - core/test/chain-rule.test.ts: 6 new tests, all passing. They cover create, attach, adopt, a human move counted as accepted, a system move counted as a violation, and two labs on one goal from before the rule.
  - Four older core tests built two labs on one chain. I changed their setups to use a free goal, or to write that state straight into the table.
  - The full core suite, run before my last fixes, had 931 passing and only those 4 failing; afterwards I re-ran just the four fixed files, all passing.
  - Server tests rest, access and captain-rights: 40 passing.
  - Typecheck is clean.
- **Docs.** docs/goals.md has a new "One building per chain" section and no longer says "several buildings may share a goal". The log entry is docs/log.d/2026-11-12-pix-2-chain-rule.md. The topic page is [dc_ud8fgrr2z2](../../wiki/2026-11/2026-11-12-chain-rule-gr-2r17x8egrc-step-1-kr-ig32y08ihi-8fgrr2z2.md).
- **What is left:** merge PR #436, wait for its deploy, then read the boot event live and file it as the evidence for kr_ig32y08ihi.

## What I need from you
Nothing needed.
