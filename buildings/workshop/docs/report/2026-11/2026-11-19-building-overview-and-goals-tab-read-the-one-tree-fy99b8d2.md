---
id: "dc_upfy99b8d2"
type: "report"
state: "building"
title: "Building Overview and Goals tab read the one tree: PR #523 open (draft)"
authorId: "ag_z7ruxtsmcm"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Step 4 built, PR #523 open as a draft. The town merges it when green (merge wait queued); the live check, screenshot and close go on the queue as the grant's last session, held until Mitchell decides the gate."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-19T17:41:59.947Z"
sessionId: "se_hdi6drx456"
assignmentId: "as_an0dx2en5a"
costUsd: 4.171349499999999
tokens: 208567
turns: 20
createdAt: "2026-11-19T17:40:46.541Z"
updatedAt: "2026-11-19T17:41:59.947Z"
---
## What I did
Built step 4 of gr_h4m0lyhb1f and opened draft PR #523 (https://github.com/mitchellgordon95/muster-town/pull/523). I did not park on it, because the grant is held at its gate and no new session can start. I also checked steps 2 and 3 on the live server (daaccbbd, up since 17:29:04Z).

## Findings
- **Overview Goals line** now reads "N goals, N grants funded, N of N key results met", counted over the building's subtree (`goalsSummary` in panels/keyResults.ts):
  - Funded counts grants that are funded or held at their gate.
  - The key-result count leaves out key results on drafts and rejected proposals.
  - Met counts met and met-unverified.
  - The "outside this goal" caveat is gone from the Grants line.
- **Goals tab** shows the subtree goal by goal:
  - Each goal is a link into the goal tree. Under it come the grants filed on it, from any building, each with its status and its key results.
  - Key results are drawn by the goal tree's own `KrLines`, so the words match the goal tree page.
  - Closed grants are folded under "Closed". A goal with nothing under it says "No grant under it". Child goals are indented.
  - Met and Missed stay in place for `building.fund` holders. The old flat list and its grant-word column are gone.
- **New API:** `GET /api/buildings/:id/grants?subtree=1` (core `Grants.list({subtree})`) returns every grant filed on a goal in the subtree. The mock follows.
- **docs/goals.md** describes what runs now:
  - The "Until this is built…" status line is gone.
  - New sections: the model, the data model (no objectives or KR buildingId), and "The building panel reads the tree".
  - The migration plan, build order, UI inventory, open questions and skip-levels went; git history keeps them.
  - There is a log.d entry.
- **"objective" sweep:** no UI label says objective any more. The dead `.kr-objective*` CSS is removed. The grant's own `objective` field is kept, as Pix decided.
- **Checks:** typecheck, check:docs and knip (pre-push) pass. Tests pass: web 450, server 359, and core grants.test.ts 18, including a new subtree test. CI on #523 has not run yet.
- **Live checks on daaccbbd:**
  - GET /api/buildings/workshop/grants returned 31 grants, none with keyResultId or keyResult.
  - GET /api/grants/gr_h4m0lyhb1f lists key results with grantId and a status from the five words, and no evidence, buildingId or objectiveId field.
  - So I claimed kr_jwuf0g9iow and kr_awya2qdkou.
- **Not done:**
  - No screenshot of the Workshop panel: this desk has no browser, and the change is not live yet.
  - kr_4ee59lp0m2 stays open until #523 is merged and live.
  - **Key results:** kr_zcwoxvsssi, kr_awya2qdkou and kr_jwuf0g9iow can be claimed now. kr_4ee59lp0m2 can be claimed once #523 is live, after the Overview line and the Goals tab are compared with the goal tree page.

## What I need from you
Once Mitchell decides the gate, merge PR #523 when it is green. Then a short session should check the Workshop panel live, take the screenshot and close the grant.
