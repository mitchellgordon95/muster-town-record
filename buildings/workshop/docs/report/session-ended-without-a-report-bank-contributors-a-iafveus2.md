---
id: "dc_ebiafveus2"
type: "report"
state: "building"
title: "Session ended without a report: Bank contributors and funding (Sage): add a top-contributors-by-tokens leaderboard in the Bank. Remove the Town Hall don"
authorId: "ag_x87ckq8vc1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Workshop standup\": Once the Bank is live, Sage wires the donation panel into the app and renderer."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-20T19:53:00.624Z"
sessionId: "se_9m8qqpg2cx"
assignmentId: "as_fst0rp1y18"
costUsd: 1.7222534
tokens: 3284870
turns: 52
createdAt: "2026-10-20T19:41:50.935Z"
updatedAt: "2026-10-20T19:53:00.624Z"
---
## What I did
Assignment: Bank contributors and funding (Sage): add a top-contributors-by-tokens leaderboard in the Bank. Remove the Town Hall don. The session ended without `submit_report`; this is a fallback report written by the runtime.

## Findings
I'm holding until Root pushes the Bank building to main. The background watcher will wake me when `layout.ts` or `app.tsx` changes on origin.

So far:
- **On main:** two commits, `47ec91c` and `7b112d2`. They add the top-contributors data to the Bank summary, the web Bank API with a mock, and new Bank sections: the leaderboard, a donate form, the list of funding inputs and the share controls.
- **Ready locally, not pushed yet:** the Town Hall donation box is removed (core layout and furniture, the old panel, the mock, tests and docs). Core tests pass, 155 of 155. The last steps are wiring the `donation` panel kind, `app.tsx`/`state.ts`/the renderer, and Root's BankPanel. They wait until Root's push lands so we don't collide.

## What I need from you
Nothing needed.

