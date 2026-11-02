---
id: "dc_b2m20wwdpg"
type: "report"
state: "building"
title: "da7c5b3 is live: Goals and Grants tabs work on muster.town, board is notes only; live Goals screenshot mf_wizrh4ch8o for rollup 30"
authorId: "ag_rc1r2andfp"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_flhly0kldr","dc_72nexb0bwn","dc_hzqgqqeqho"],"urls":["https://muster.town/api/health"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "da7c5b3 live-checked as guest: Overview lines open Goals/Grants, 3 funded KRs, Grants tab lists real step assignments with tokens, board notes only, web tests 121/121. Live Goals screenshot mf_wizrh4ch8o goes into rollup 30. Edit/Settings needs a manager sign-in: Mitchell can check it himself from the Goals tab (rollup 30 Your call)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T05:12:28.812Z"
sessionId: "se_l3vuih7s2e"
assignmentId: "as_gyejjnke7q"
costUsd: 0.8766042000000002
tokens: 43830
turns: 27
createdAt: "2026-10-29T05:12:13.864Z"
updatedAt: "2026-10-29T05:12:28.812Z"
---
## What I did
- Confirmed with `/api/health` that live is on da7c5b3. 9f4bc24 is on main after it; it is not needed for this check.
- Ran the web tests in the foreground on 9f4bc24: **121/121 pass** in 36 s.
- Drove the live site as a guest with playwright-core and chromium. There is no URL for a building, so I opened `#/grant/gr_iq5m7dug56` and clicked "Town Workshop" in its subtitle to reach the building panel.
- Took one cropped live screenshot and rewrote the topic page [dc_72nexb0bwn](../../wiki/2026-10/2026-10-28-objectives-key-results-and-kpis-code-nexb0bwn.md) with the live state.
- Changed no code and opened no PR.

## Findings
- **Overview lines open the tabs (live):** "Goals: 3 objectives, 5 key results, 3 funded →" opens Goals, and "Grants: 0 proposals, 3 funded, 3 closed or held →" opens Grants. The building goal now has 5 key results, not 4.
- **Goals tab:**
  - Key results 1, 3 and 5 show **FUNDED**. Those are the ones with grants gr_iq5m7dug56, gr_jh0lu0w6yj and gr_tvt32g9xly.
  - Key results 2 (Town blockers) and 4 (visitor starter) show **OPEN**.
  - Each key result shows its status pill, how to check, and its status note.
- **Grants tab** lists the real step assignments, each with its adjusted tokens and session count. For example, gr_jh0lu0w6yj shows steps 1–5, including step 4's dead first attempt at 0 tokens and the step 5 that is running now. Below that, "Checkpoint and closed" lists the 3 rejected proposals.
- **The board is notes only (live):** the board shows its header text, the 4 town-wide FYIs, then "No FYIs on the board". The goals block is gone.
- **Not checked on the live site:** the Edit button and Settings, because a guest can't see them and checking needs a signed-in manager. In the code, `KeyResultsEditor` now appears only in `GoalsTab.tsx` (line 47), and Settings no longer has it.
- **Picture for rollup 30:** ![Live Workshop building panel, Goals tab (da7c5b3)](/api/media/mf_wizrh4ch8o.png) mf_wizrh4ch8o (500×300, live). It replaces the mock screenshot mf_w4n9d5npww. The Grants picture is still the mock mf_dk6ikumgtq.
- **One thing that looks odd:** key result 1's status note is about 1,500 characters and takes up most of the Goals tab. It is shown whole on purpose, under the no-truncation rule. Shorter notes would fix it; the code doesn't need to change.

## What I need from you
Nothing needed.
