---
id: "dc_4nz8b57os7"
type: "report"
state: "building"
title: "Finance page built (draft PR #61, on top of #60): used, expired, left, sum check, 30-day projection, overdrawn pools"
authorId: "ag_t5p8jfp9fk"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Good work. Step 2 done. I'm asking Mitchell to merge #61 (which includes #60) in one go and redeploy. Step 3 (live check + evidence for the checkpoint) is queued for you and waits for the next deploy."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-27T19:07:09.052Z"
sessionId: "se_24cywssr1c"
assignmentId: "as_8pqynhtvq4"
costUsd: 1.1512959999999999
tokens: 57565
turns: 34
createdAt: "2026-10-27T19:06:00.046Z"
updatedAt: "2026-10-27T19:07:09.052Z"
---
## What I did
I built step 2 of gr_gi5jbgzv4k, the public Finance page, on top of the PR #60 branch. To do that I merged the #60 branch into mine and resolved a conflict in docs/log.md. Then I committed b070f2f and opened draft PR #61: https://github.com/mitchellgordon95/muster-town/pull/61. I did **not** merge it. #61 contains #60, so merging #61 would also merge #60, and your note says Mitchell decides #60. Nothing is live yet, so I have no screenshot of the live page.

## Findings
- **Where to find it:** a new "$" button in the HUD bar (next to the dashboard ▤), or the link `#/finance`. No sign-in is needed. The page reads `GET /api/finance` in the shape that shipped in #60, plus `/api/bank` for the pools.
- **Summary card:**
  - Total received, split into credited and donated.
  - Used, expired and left.
  - Overdrawn, on its own red line when it is above 0.
  - The sum check written out in numbers, e.g. "✓ Adds up: used … + expired … + left … = X; total … + overdrawn … = X". When it fails it turns red: "✗ Does not add up (off by N)". The identity is the one that shipped, which includes overdrawn as you asked.
- **Next 30 days:**
  - The burn rate, labelled with how many days it averages (the last 7, or fewer while the history is shorter).
  - Projected use over 30 days.
  - How many days the tokens left last at that rate.
  - A note that new credits and renewals are not counted.
- **Bank pools:** each pool shows "Expires today" and "Permanent". Permanent is max(0, durable), with "overdrawn by N" under it when durable is negative. On live, the General pool should show 0 and "overdrawn by 256,870" ([dc_myhlhsevgz](2026-10-27-general-pool-s-negative-durabletokens-256-870-is-o-hlhsevgz.md)).
- **Checks:**
  - New `packages/web/test/finance.test.tsx` covers the sum check text (passing and failing), the pool clamp, the runway, and a server-side render of the whole page.
  - All 80 web tests pass, `npm run typecheck` is clean and `check:docs` is OK.
  - The test caught a test fixture of mine that didn't add up, so the sum check line does what it should.
- **Docs:** I updated docs/architecture.md and docs/log.md. The mock API serves a matching toy finance summary.

## What I need from you
Decide whether PR #61 can be merged with #60 (or after it), then redeploy. Step 3 (checking muster.town/workshop/#/finance live, then the checkpoint) waits on that.
