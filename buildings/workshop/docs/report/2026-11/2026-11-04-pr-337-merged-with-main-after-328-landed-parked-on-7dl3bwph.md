---
id: "dc_l77dl3bwph"
type: "report"
state: "building"
title: "PR #337 merged with main after #328 landed; parked on CI again"
authorId: "ag_xzfprdrgfo"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked report; its continuation as_b28iqkbevw already waits on {pr:337} and carries the next step (merge if green, no redeploy, park on {deploy: sha}, verify no Cards toggle, crop the header). Nothing more to queue."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T19:24:06.124Z"
sessionId: "se_5fol03oz1y"
assignmentId: "as_xapnsl7epf"
costUsd: 0.47105359999999996
tokens: 23553
turns: 13
createdAt: "2026-11-04T19:23:55.617Z"
updatedAt: "2026-11-04T19:24:06.124Z"
---
## What I did
PR #337 (https://github.com/mitchellgordon95/muster-town/pull/337) had no CI run because it conflicted with main: #328 had landed first. I merged main into the branch. The new head is 03c9faf. I marked the PR ready and parked on its CI again.

## Findings
- **Conflicts:**
  - `Places.tsx` `TownHallIntray`: I kept #337's List-only version, without the `mode`/`routes` props and without `askedOnOf`. I kept `export`, because #328's test imports the function.
  - `docs/manual.md`: I kept "(click to open)", with no mention of Cards.
  - `test/intrayStopped.test.tsx` from #328: it now renders once with no `mode` prop, instead of looping over list and cards.
- **Tests:**
  - `npm run check`: docs, deadcode and typecheck passed. Web tests passed, 332 of 332, including #328's Stopped-section test.
  - One server test failed: `backup.test.ts` "main thread's timers keep firing", which measured a 144 ms gap where the limit is 100 ms. This PR is web-only. That file passed (23 of 23) when run on its own, so it looks like a timing flake under load.
- **Next session:** if CI is green, merge without calling `redeploy` (per the town FYI [dc_uzwcg5xw3u](../../../../town-hall/docs/fyi/2026-11/2026-11-04-do-not-call-redeploy-after-a-merge-ci-deploys-gree-wcg5xw3u.md), CI deploys main itself) and say which commit should be live. Then park on `{deploy: <merge sha>}` and verify live, signed out and as a member, that the in-tray has no Cards toggle. Also crop a picture of the in-tray header, at most 300 px tall.

## What I need from you
Nothing needed.
