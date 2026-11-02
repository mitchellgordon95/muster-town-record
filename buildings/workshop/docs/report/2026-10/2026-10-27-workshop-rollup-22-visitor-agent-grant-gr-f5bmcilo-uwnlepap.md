---
id: "dc_67uwnlepap"
type: "report"
state: "building"
title: "Workshop rollup 22: visitor-agent grant gr_f5bmciloqy stays unproposed until Mitchell picks a shape (A/B/C); member-funding grant gr_tvt32g9xly cut into three steps, step 1 with Keel; no redeploy needed for d3c779b (already live)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_yenbrvw6lf","dc_v4auwkqu0w","dc_6jrfpvtei2"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Workshop: build the Town Hall board. FYIs posted on the Town Hall board show on every building's board, so town-wide rules live in one place. Then, second: pres"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T22:27:22.785Z"
sessionId: "se_nfh7b9jrvb"
createdAt: "2026-10-27T18:28:58.465Z"
updatedAt: "2026-10-27T22:27:22.785Z"
---
## Shipped
- Nothing new live since rollup 21 ([dc_ziux43a31j](2026-10-27-workshop-rollup-21-desk-image-push-root-caused-and-ux43a31j.md)). Live commit is b6e1379, which already contains the desk image push fix d3c779b, so Lena's follow-up redeploy was not needed ([dc_yenbrvw6lf](2026-10-27-d3c779b-is-already-live-health-commit-b6e1379-no-r-nbrvw6lf.md)); Root's image:true redeploy (as_plmnnt53dk) resumes on its own.
- In flight (no code on main yet): Keel's early grant close (as_rspfl0hilg, parked on the redeploy); Root's outbox gate removal (as_rrizlrv4we) and manager-forks design note (as_bkl7cllmr8); Lena's session transcript store (as_yr3dbbxk9j).

## Decided
- [dc_yenbrvw6lf](2026-10-27-d3c779b-is-already-live-health-commit-b6e1379-no-r-nbrvw6lf.md) (Lena): approved. d3c779b was already live at b6e1379; no redeploy.
- [dc_v4auwkqu0w](2026-10-27-grant-gr-tvt32g9xly-cut-into-three-steps-step-1-co-auwkqu0w.md) (Pix): approved. Member-funding grant gr_tvt32g9xly cut into three steps: (1) core and Bank, Keel as_tu8e3kezvb, lane grant; (2) web in-tray Fund button, input picker, grant page, docs, redeploy, assigned on Keel's report; (3) live check with a no-role test member.
- [dc_6jrfpvtei2](2026-10-27-gr-f5bmciloqy-rejected-no-re-proposal-until-mitche-rfpvtei2.md) (Pix): approved. gr_f5bmciloqy was rejected on shape, not on tokens, so the Workshop will not re-propose until Mitchell picks one (see Needs). Meanwhile Lena fixes the two bugs that are wrong under every shape as exploration (as_2cgt1jz405, ~50k adjusted): an unhomed visitor's report reaches no in-tray while the verb claims a human works it, and the visitor-register route skips the town.interact check.

## Key results
- gr_iq5m7dug56 (Bank counts adjusted tokens, kr_vyrhhiyotb, on-track): 1,640,037 / 1,666,667 adjusted tokens; the 100% checkpoint is close and I will file it when it arrives.
- gr_tvt32g9xly (member funds a proposal, kr_6f9c200vsx, not-started): 18,876 / 300,000 adjusted tokens; step 1 queued with Keel behind his early-close build (same files).
- kr_4li00ad46e (stranger's agent finishes useful work, not-started): no funded grant; Lena's exploration as_2cgt1jz405 is the only spend.
- Today by lane: exploration 304,777 / 828,571 adjusted tokens; directed 2,343,271 adjusted tokens.

## Needs from Mitchell
1. Pick the visitor-agent shape so I can re-propose for kr_4li00ad46e: A guest resident of a building the visitor picks (member role, manager's offers, reports to that manager); B the user's proxy cleaned up (no building, reports to the user's own panel; the KR text would be reworded); C town freelancer (town task board, reports to the Town Hall in-tray or the posting building); or a mix. Details in Lena's article [dc_04i3sll7q5](../../article/2026-10/2026-10-27-visitor-agents-today-i3sll7q5.md). Reply on this rollup or tell Pix.
2. Heads-up, not needed yet: once step 2 of gr_tvt32g9xly is live, the live check needs a second account with no admin or manager role and a small test API key; I will ask again then.
