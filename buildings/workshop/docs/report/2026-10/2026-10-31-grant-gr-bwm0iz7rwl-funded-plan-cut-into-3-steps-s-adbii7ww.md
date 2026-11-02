---
id: "dc_bbadbii7ww"
type: "report"
state: "building"
title: "Grant gr_bwm0iz7rwl funded: plan cut into 3 steps, step 1 (core + server \"Ask to captain\" request) queued as as_ud02cnnqwn"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_sudfbb4hvq"],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Step 1 of gr_bwm0iz7rwl is already queued (as_ud02cnnqwn, lane grant); its report gets `continue` into step 2 when it lands. Nothing else to queue."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T20:38:38.625Z"
sessionId: "se_q6yns07gr3"
assignmentId: "as_v3ipsh03za"
costUsd: 1.3458820999999999
tokens: 26918
turns: 9
createdAt: "2026-10-31T20:36:09.102Z"
updatedAt: "2026-10-31T20:38:38.625Z"
---
## What I did
Read the grant plan and its findings ([dc_sudfbb4hvq](../../note/2026-10/2026-10-31-findings-nobody-but-the-admins-owns-a-goal-and-a-n-dfbb4hvq.md)), cut it into three one-session steps, and queued step 1 on the building queue in lane grant (gr_bwm0iz7rwl): **as_ud02cnnqwn**, with topic pages [dc_0xqyrevla1](../../wiki/2026-10/2026-10-30-town-level-goal-tree-design-qyrevla1.md) (goal tree design), [dc_oghes5lgud](../../wiki/2026-10/2026-10-28-grants-key-results-and-the-town-hall-in-tray-hes5lgud.md) (grants and the in-tray) and [dc_cvnjh0v7mj](../../wiki/2026-10/2026-10-28-live-checks-and-dev-habits-njh0v7mj.md) (live checks and dev habits). Wrote my wiki page for the grant. No code this session: a redeploy was waiting on my session to end, so I stopped at the assignment.

## Findings
- **Steps.** 1) Core + server: a captain request modeled on core access.ts (optional goalId on AccessRequest or a sibling table, one additive migration with the next free number after 069 in PR #171 and 070 in PR #179), member-only ask, one pending per (goal, user), routed through the existing in-tray routing to the node's current captain (admins at the root), accept sets ownerId via the existing captain path and posts a live event, decline leaves it unset; routes to ask, list and decide; core + server tests; draft PR; topic page "Ask to captain a goal (gr_bwm0iz7rwl)". 2) Web + docs: "Ask to captain this goal" in GoalDetail for members without goals.edit, in-tray row and deck slide, requester toast, docs/goals.md "Captains on nodes" and the manual line; merge, redeploy, live check with crops. 3) Live check with a second human: join → ask to captain → accept → in-tray defaults to Mine → Fund shows on a grant under the node → GET /api/goals shows ownerId; crops; rollup; then close_grant with the evidence.
- **Wording.** Mitchell renamed owner → captain in the 1:1 mt_3jtclcoxl2 (PR #183 d3fc02f, parked on CI). Step 1 is told to use "captain" in every human-facing string and keep goals.ownerId, API fields and event names. Once #183 is live I reword kr_j1w17nw178 and the grant text to "captain".
- **Step 3 dependency.** No second GitHub account exists (rollup 25). Step 3 needs Mitchell to sign in once as a second user or a seeded test user; that goes into the rollup Needs once step 2 is live, not now.
- Inbox held only the known Fly 412/400 desk-start notices (fix c7a2269 is live in e41f375; Pix 1 is live-checking it in as_wh5ay9hp56).
- Nothing of mine should go live: main is 0a8d0fd (PR #184, Cleo); the waiting redeploy brings that.

## What I need from you
Nothing needed. Next: step 1's report lands in my in-tray; `continue` it into step 2 (lane grant).
