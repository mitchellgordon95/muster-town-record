---
id: "dc_zgbcla6udu"
type: "report"
state: "building"
title: "Hollyville retire: PR #353 lets a Workshop admin retire any hosted collective; parked on CI"
authorId: "ag_174xk6if1j"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked on CI for #353; its continuation as_8obvgooj2m (merge when green, no redeploy) is already on the queue, so nothing more to assign. Retire only, no hard delete (right call: Hollyville's hub owner is @edwadli, not Mitchell). Lands in rollup 49 with the rename and the bulletin board once live; Your call there = Mitchell clicks Planning desk > System > Hosted collectives > Retire Hollyville."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T19:01:47.041Z"
sessionId: "se_cfl1a7yglb"
assignmentId: "as_xyejr0kojv"
costUsd: 0.8455556
tokens: 42278
turns: 20
createdAt: "2026-11-05T19:01:17.897Z"
updatedAt: "2026-11-05T19:01:47.041Z"
---
## What I did
- Checked who owns Hollyville. The hub row's owner is @edwadli (us_qk4w3bq1az), not Mitchell. The only retire path today is the hosted `POST /hollyville/api/collective/retire`, and its gate is that collective's own admins: a hosted app is built with `admins: []` (main.ts:118). Its button is at Planning desk > System > "This collective" (PlanningPanel.tsx `ThisCollective`). So Mitchell couldn't retire it.
- Built a way for Mitchell to retire it, in PR https://github.com/mitchellgordon95/muster-town/pull/353 (draft, head on branch agent/pix-2/delete-the-hollyville-test-collective-mi):
  - Root route `POST /api/collectives/:slug/retire`, open to Workshop admins only. It calls the existing `hub.retire`.
  - Planning desk > System now has a "Hosted collectives" section for Workshop admins. Each collective has "Retire…", then "Retire X for good".
  - New test in packages/server/test/hub-start.test.ts. hub-start passes 11/11, web passes 336/336, typecheck is green.

## Findings
- Live today, GET /api/collectives lists hollyville ("Make money", never started) and trauma. /api/join-funnel shows Hollyville active since 2026-10-29, with no key and no sessions.
- I can't retire it with town credentials: `requireUser` refuses agent tokens. Once #353 is live, Mitchell clicks: **muster.town/workshop → Planning desk → System → Hosted collectives → Retire… next to Hollyville → Retire Hollyville for good.**
- What retire leaves behind:
  - The hub.db row stays with state 'retired', and the slug is never reused.
  - /hollyville/ returns 410 with a retired notice, and the homepage stops listing it.
  - The directory hosted/hollyville/ stays on disk (collective.json, data/town.db, export/), and so do its backups.
  - No hard delete was done; that needs Mitchell's word.
- Next (continuation): when CI is green, mark #353 ready and merge it (no redeploy; CI promotes it), then report the merge commit.

## What I need from you
Nothing needed yet. Once #353 is live, Mitchell clicks the path above.
