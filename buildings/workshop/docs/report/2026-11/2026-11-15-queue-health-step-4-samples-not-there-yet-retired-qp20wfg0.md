---
id: "dc_kaqp20wfg0"
type: "report"
state: "building"
title: "Queue health step 4: samples not there yet; retired-before-read fix in PR #466, parked on CI"
authorId: "ag_vfymdsgsmy"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-15T23:13:33.582Z"
sessionId: "se_k4wrs4eypg"
assignmentId: "as_p9l5n54ed2"
costUsd: 0.6712105000000002
tokens: 33561
turns: 19
createdAt: "2026-11-15T23:13:33.567Z"
updatedAt: "2026-11-15T23:13:33.582Z"
---
## What I did
I read live /api/health at commit 7e1a38aa (startedAt 2026-11-15T23:02:17Z), at 23:11Z. I traced the "asks retired before anyone read them" row in core measures.ts. I fixed it, added a test, and opened draft PR #466.

## Findings
- The step's precondition is not met. Step 1 went live today, and Mitchell has not yet worked the queue on two days. `legible.queue` has sample 0 for minutes on card for money, click, policy and credential asks. Do asks: 3.51 min median, n=5, 0 questions. Gates: 0.88 per funded grant (35/40). Budget used: 0.69 (21.7M of 31.3M). Warning: false. screenViews: 10 views by 1 user.
- "Retired before read 60 of 60" was a bug, not just old data. The `seen` table gets ask rows only from GET /api/asks/:id (routes/asks.ts:23). The decision queue never calls that route. So no ask retired through the queue could ever count as read.
- Fix (PR #466, https://github.com/mitchellgordon95/muster-town/pull/466): an ask now counts as read if a screen view of the ask or of its target was opened while the ask was live. The core measures.test.ts test covers a third ask retired after its target was in focus: 3 retired, 1 unread. That test passes, and so does `npm run typecheck`.
- Topic page [dc_271txc8zem](../../wiki/2026-11/2026-11-12-queue-health-gr-pdja05z2f1-1txc8zem.md) now has the step 4 plan: merge #466, re-read on 11-17 or later, compare three asks by hand, judge the 30-min cap and the 0.5 / 0.85 thresholds, and check the rank run block (kr_nsghrfza2i).
- No key result can be claimed yet. kr_i7ibeasoff needs money and click samples above 0.

## What I need from you
Nothing needed.
