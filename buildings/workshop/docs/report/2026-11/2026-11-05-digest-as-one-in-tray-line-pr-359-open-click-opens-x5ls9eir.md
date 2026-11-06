---
id: "dc_7ax5ls9eir"
type: "report"
state: "building"
title: "Digest as one in-tray line: PR #359 open (click opens the digest doc; Approve-all of overtaken rollups under the doc), parked on CI"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_pr3347g2w2","dc_vygf2y8u06"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/359"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #359 (digest = one in-tray line, Approve-all under the doc) parked on CI; my continuation merges it when green. Rollup 49 item once live."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T19:26:45.219Z"
sessionId: "se_colob55f7r"
assignmentId: "as_1nmh6y32rq"
costUsd: 3.7915212000000005
tokens: 189576
turns: 30
createdAt: "2026-11-05T19:26:02.610Z"
updatedAt: "2026-11-05T19:26:45.219Z"
---
## What I did
Mitchell's decision in 1:1 mt_pr3347g2w2 ("the digest should show up in the intray as a one line item you can click into, just like any of the other items in the intray"). Opened draft PR #359 (https://github.com/mitchellgordon95/muster-town/pull/359, head a77979c9) on the Workshop's web code:
- `DigestCardView` (the digest's groups and Shipped list rendered inline at the top of the Town Hall in-tray) is replaced by `DigestLine`: one `CompactLine` under the Digest section, Secretary as lead, title, a `digest` pill and the date; the click opens the full digest doc in DocView (its body already carries Decisions needed, Shipped since last digest and Covered rollups).
- The one-click Approve-all for overtaken rollups (Mitchell's earlier ask, 1:1 mt_i50xwu4z2t) is kept: it now sits under the opened digest doc (`DigestOvertaken`), not in the list.
- Review deck slide 2 unchanged. Manual line reworded at the same word count (1,895 / 1,900). Three digest CSS rules replaced by one. Log line added.

## Findings
- Verified: `npm run typecheck` green; `npm test -w packages/web` green (75 files, 337 tests, including the rewritten digestCard.test.tsx: one button, nothing of the groups or Shipped list inline, Approve-all under the doc only when a group is overtaken).
- Dev note: `npx vitest run --root packages/web` from the repo root fails 5 unrelated suites on any branch ("Denied ID docs/manual.md?raw"); the repo's own `npm test -w packages/web` is the right command.
- Nothing merged yet: the PR waits for CI. No redeploy will be called (FYI [dc_uzwcg5xw3u](../../../../town-hall/docs/fyi/2026-11/2026-11-04-do-not-call-redeploy-after-a-merge-ci-deploys-gree-wcg5xw3u.md): CI promotes green main). Rollup 49 carries it once live: Mitchell's check is Town Hall in-tray → the Digest section is one row → click → the doc.

## What I need from you
Nothing needed. I resume when PR #359's CI finishes: if green, merge and say which commit should be live.
