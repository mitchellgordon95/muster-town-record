---
id: "dc_e7mjlbazn6"
type: "report"
state: "building"
title: "Workshop rollup 33: goal tree steps 1-5 live on e3da989 (map from the tree, Town Hall goal editor, in-tray goal proposals, Change this goal, Planner); Bank yes needed for the Planner and steps 7-8"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_vbylnhsi2m","dc_kira3d2fbc","dc_vptlvfj2db","dc_gz8571foot","dc_f3ue446bxn","dc_cmvzu4j6aj","dc_oyvkqa06g6","dc_9geoa9phoa","dc_7xm0lcxcrf","dc_6z4hcj8ljf","dc_jaii2zxeqb","dc_m32jxdc4a7","dc_bkwozc2bpa","dc_n7uvptybqt","dc_gmjz5bmxwq","dc_5ntnc3u8go","dc_k76m4lhs9a","dc_syd8drel26","dc_f8pc0dfbr6"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-31T01:05:15.461Z"
sessionId: "se_kt2z4l85a9"
createdAt: "2026-10-30T23:56:55.514Z"
updatedAt: "2026-10-31T01:05:15.461Z"
---
Live commit e3da989 (health 23:53Z 10-30). Everything from the 1:1 mt_kh0zaqui0w build order through step 5 is live; step 6 (postmortems on missed key results, kanban) is running now. No migration beyond 061 (additive), no Bank code touched.

## Shipped

**1. The goal tree is the town's one plan, and the map is drawn from it (steps 1 and 2)**
**What it is:** The town goal tree from docs/goals.md lives in the database (16 goals, every building attached to exactly one node, the root = the town goal). The map is generated from the tree: Town Hall at the root, one plaza with a signpost per goal, roads along the edges, each building standing at its goal; drag placement is gone. PRs #116, #122, #123, #124 (def72e8, 0122bf1, 5ea10f0); reports [dc_vbylnhsi2m](2026-10-30-every-key-result-the-town-has-had-31-gathered-in-d-ylnhsi2m.md), [dc_kira3d2fbc](2026-10-30-docs-goals-md-fourth-pass-map-drawn-from-the-goal-ra3d2fbc.md), [dc_vptlvfj2db](2026-10-30-docs-goals-md-fifth-pass-q5-q7-and-the-key-rule-fo-tlvfj2db.md), [dc_gz8571foot](2026-10-30-goal-tree-step-1-merged-pr-122-def72e8-tree-tables-8571foot.md), [dc_f3ue446bxn](2026-10-30-goal-tree-step-1-live-on-def72e8-16-goals-every-bu-ue446bxn.md), [dc_oyvkqa06g6](2026-10-30-goal-tree-step-2-merged-pr-123-0122bf1-the-map-is-vkqa06g6.md), [dc_9geoa9phoa](2026-10-30-goal-tree-step-2-live-on-0122bf1-the-map-is-the-tr-eoa9phoa.md), [dc_7xm0lcxcrf](2026-10-30-bank-marquee-moved-off-the-town-hall-s-wall-pr-124-m0lcxcrf.md), [dc_6z4hcj8ljf](2026-10-30-bank-marquee-live-on-5ea10f0-clear-of-the-town-hal-4hcj8ljf.md).
**What you'd see:** Open the map: 16 signpost plazas, the Town Hall at the root plaza, the Workshop at "Ship improvements to the core experience". The old planning PUT route answers 404. The Bank marquee no longer overflows.
![Map generated from the goal tree](/api/media/mf_x8tgzt6cm8)
**Your call:** Two looks I chose without you: an empty goal is an empty plaza with a signpost, and long walks between distant goals are not folded. Say if either should change. The key result inventory ([dc_io1ry1ryjz](../../note/2026-10/2026-10-30-every-key-result-the-town-has-had-31-for-sorting-i-1ry1ryjz.md), 31 rows, blank "Standing goal?" column) waits for your sort whenever you want.

**2. The Town Hall goal editor (step 3)**
**What it is:** A wall chart of the tree in the Town Hall (press E), with goal detail Edit / Add goal / Add key result / Move / Owner / Retire / Met / Missed, proposal cards with Accept / Edit and accept / Cut, and History and Subtree tabs; History lines carry dates. Guests see it read-only. Retiring a goal with open key results asks for a sibling to move them to. PRs #125, #126 (b01e71d, 92df5fb); reports [dc_jaii2zxeqb](2026-10-30-goal-tree-step-3-merged-pr-125-b01e71d-the-town-ha-ii2zxeqb.md), [dc_m32jxdc4a7](2026-10-30-goal-tree-step-3-live-on-b01e71d-town-hall-goal-ed-2jxdc4a7.md), [dc_bkwozc2bpa](2026-10-30-goal-tree-history-shows-dates-pr-126-92df5fb-redep-wozc2bpa.md), [dc_n7uvptybqt](2026-10-30-92df5fb-live-goal-editor-history-stamps-carry-the-uvptybqt.md).
**What you'd see:** Town Hall, press E: the wall chart; click a goal for its detail and the buttons above.
![Town Hall goal editor](/api/media/mf_vfbr4jzb9b)
**Your call:** Sign in and try Edit on a goal; no agent has done a signed-in edit (desks are guests). Say whether the building Goals tab's old editor should go read-only now that the Town Hall one exists.

**3. Goal proposals in the in-tray and deck, owner funding, "Change this goal" and "Plan with an agent" (steps 4 and 5)**
**What it is:** Manager goal proposals show in the Town Hall in-tray and the review deck, with Mine / All views; a goal's owner decides on grants in their subtree; each goal has a read-only Spend tab. "Change this goal" takes your note, opens one directed prep assignment per attached building, marks open key results under review (Keep / Move / Archive), and opens a Town Hall planning meeting when every prep report is in or after 24 h. "Plan with an agent" opens a 1:1 with the Planner, a Town Hall resident, who answers with proposal cards. PRs #127, #128 (c91e60d, e3da989); reports [dc_gmjz5bmxwq](2026-10-30-goal-tree-step-4-merged-pr-127-c91e60d-goal-propos-jz5bmxwq.md), [dc_5ntnc3u8go](2026-10-30-goal-tree-step-4-live-on-c91e60d-spend-tab-renders-tnc3u8go.md), [dc_k76m4lhs9a](2026-10-30-session-ended-without-a-report-goal-tree-build-ste-6m4lhs9a.md), [dc_syd8drel26](2026-10-30-goal-tree-step-5-merged-pr-128-e3da989-change-this-d8drel26.md), [dc_f8pc0dfbr6](2026-10-30-goal-tree-step-5-live-on-e3da989-goal-changes-200-pc0dfbr6.md). API-visible only for guests, so no third picture (the two-picture cap; the Spend crop mf_7agdsz23d9 is on file).
**What you'd see:** Town Hall in-tray: goal proposals as cards, Mine / All. Goal detail: Spend tab (this building's Bank objective, 7 days: 3.1M adjusted tokens over 37 sessions), "Change this goal" and "Plan with an agent" buttons when signed in. GET /api/goal-changes?open=1 returns 200 with no open changes.
**Your call:** Try "Change this goal" on a test goal, or "Plan with an agent". The Planner cannot start yet: it posts a can't-start notice, because the Bank gives the Town Hall no pool to draw from (see Needs). The reorg meeting then falls back to the first manager as facilitator.

## Decided
- [dc_vbylnhsi2m](2026-10-30-every-key-result-the-town-has-had-31-gathered-in-d-ylnhsi2m.md) → approve (key result inventory, 31 rows)
- [dc_kira3d2fbc](2026-10-30-docs-goals-md-fourth-pass-map-drawn-from-the-goal-ra3d2fbc.md) → approve (PR #116 fourth pass)
- [dc_vptlvfj2db](2026-10-30-docs-goals-md-fifth-pass-q5-q7-and-the-key-rule-fo-tlvfj2db.md) → approve (PR #116 fifth pass)
- [dc_gz8571foot](2026-10-30-goal-tree-step-1-merged-pr-122-def72e8-tree-tables-8571foot.md) → approve (step 1 merged)
- [dc_f3ue446bxn](2026-10-30-goal-tree-step-1-live-on-def72e8-16-goals-every-bu-ue446bxn.md) → approve (step 1 live check)
- [dc_cmvzu4j6aj](2026-10-30-session-ended-without-a-report-goal-tree-build-ste-vzu4j6aj.md) → continue (step 2 hit the turn cap; re-queued)
- [dc_oyvkqa06g6](2026-10-30-goal-tree-step-2-merged-pr-123-0122bf1-the-map-is-vkqa06g6.md) → approve (step 2 retry)
- [dc_9geoa9phoa](2026-10-30-goal-tree-step-2-live-on-0122bf1-the-map-is-the-tr-eoa9phoa.md) → approve (step 2 map from the tree live)
- [dc_7xm0lcxcrf](2026-10-30-bank-marquee-moved-off-the-town-hall-s-wall-pr-124-m0lcxcrf.md) → approve (Bank marquee fix)
- [dc_6z4hcj8ljf](2026-10-30-bank-marquee-live-on-5ea10f0-clear-of-the-town-hal-4hcj8ljf.md) → approve (marquee fix live check)
- [dc_jaii2zxeqb](2026-10-30-goal-tree-step-3-merged-pr-125-b01e71d-the-town-ha-ii2zxeqb.md) → approve (step 3 goal editor merged)
- [dc_m32jxdc4a7](2026-10-30-goal-tree-step-3-live-on-b01e71d-town-hall-goal-ed-2jxdc4a7.md) → approve (step 3 live check)
- [dc_bkwozc2bpa](2026-10-30-goal-tree-history-shows-dates-pr-126-92df5fb-redep-wozc2bpa.md) → approve (History dates)
- [dc_n7uvptybqt](2026-10-30-92df5fb-live-goal-editor-history-stamps-carry-the-uvptybqt.md) → approve (History dates live check)
- [dc_gmjz5bmxwq](2026-10-30-goal-tree-step-4-merged-pr-127-c91e60d-goal-propos-jz5bmxwq.md) → approve (step 4 merged)
- [dc_5ntnc3u8go](2026-10-30-goal-tree-step-4-live-on-c91e60d-spend-tab-renders-tnc3u8go.md) → approve (step 4 live check)
- [dc_k76m4lhs9a](2026-10-30-session-ended-without-a-report-goal-tree-build-ste-6m4lhs9a.md) → redirect (step 5 fork died at startup during the 9a3585f deploy; retried)
- [dc_syd8drel26](2026-10-30-goal-tree-step-5-merged-pr-128-e3da989-change-this-d8drel26.md) → approve (step 5 merged)
- [dc_f8pc0dfbr6](2026-10-30-goal-tree-step-5-live-on-e3da989-goal-changes-200-pc0dfbr6.md) → approve (step 5 live check)

Queued or running: step 6 (postmortems + kanban, directed, as_i7tay9shzl); Town blockers edition 6 fires 2026-10-31 19:30Z. Nell's post-mortem follow-ups from our 1:1 mt_x40qq8poc3 are Bank Transparency's work, not listed here.

## Key results
| Key result | Grant | Status | Spent / granted |
|---|---|---|---|
| kr_vyrhhiyotb Bank counts adjusted output tokens | gr_iq5m7dug56 | on-track | 1,640,037 / 1,666,667 (100% checkpoint lands on its own) |
| kr_6f9c200vsx a member funds a key result end to end | gr_tvt32g9xly | not-started | 271,900 / 300,000 |

Today's spend by lane: exploration 31,591 / 1,000,000 tokens; directed 3,360,169 tokens (the goal tree build, from your 1:1s).

## Needs from Mitchell
1. A Bank yes, in words, for the goal tree's money steps: (a) how the Planner is paid (a one-line bank.ts change so the Town Hall's Planner draws from the General pool, or a Town Hall allocation), and (b) go-ahead to build steps 7 and 8 (funding streams with draw order and the small-donation warning; the funder filter) as Bank code. Both touch the Bank, which you reserved. Until (a), "Plan with an agent" shows a can't-start notice.

_Already waiting in your in-tray: 0 proposals, 0 requests, 1 rollup ([dc_2fo3jbdp67](2026-10-30-workshop-rollup-32-docs-goals-md-finance-rewritten-o3jbdp67.md))._
