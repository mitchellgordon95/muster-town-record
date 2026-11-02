---
id: "dc_tmq5yfhx52"
type: "report"
state: "building"
title: "Reply on rollup 5: the 22:18Z death was the subscription cap, no API-key failover happened and none could (API-key buffer overdrawn at −2.5M); fix 119bd70 records the limit message instead of \"success\""
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_mvhjrfmtxt","dc_11850gzcs5","dc_qkzqtetm8s"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Answer delivered to Mitchell; 119bd70 ships with the next deploy. The Bank top-up and the overshoot-booking question are Mitchell's (money outside the allowance): escalated in rollup 7."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-26T04:37:54.001Z"
sessionId: "se_j84z5fwjdp"
assignmentId: "as_kpblpjp612"
costUsd: 2.76081245
tokens: 51263
turns: 36
createdAt: "2026-10-26T04:37:19.974Z"
updatedAt: "2026-10-26T04:37:54.001Z"
---
## What I did
Replied to Mitchell by `tell` (twice: first read, then the confirmed answer). Scanned the whole event log (17,595 events via GET /api/events, paginated by id) for the dead session se_7n2hzzp6b5 and every session's funding, read the desk failover code (packages/desk/src/run.ts, runtime/src/desk/session.ts, core/src/bank.ts) and the Bank state. Pushed one small fix to main: 119bd70 (desk tests 18/18, typecheck clean). A redeploy was waiting on this session, so 119bd70 goes live with it or with CI's next deploy; Keel's live checks will see it. Wiki page "Desk funding and failover" (dc_qkzqtetm8s).

## Findings
- **Mitchell is right: it was the subscription, not an API key.** se_7n2hzzp6b5 started "funded by subscription", never emitted the desk's "Switching to API-key funding" status, and ended still on the subscription. The text "You've hit your org's monthly spend limit … your session limit resets 11:10pm (UTC)" is Claude Code's wording for the claude.ai plan cap (the 5-hour window). Three sessions died on it within 70 s at 22:18Z (Kelly, me, Cleo). My rollup 5 called it the "org spend limit" because that is the message's wording; same thing.
- **The failover exists and has worked before, but could not fire.** The desk reruns a limit-hit session once on AGENT_TOWN_FALLBACK_API_KEY; it fired 5 times on 10-24 23:57Z–10-25 00:05Z. The runtime only passes that key while the pool's durable (API-key) tokens are > 0 (bank.fallbackInput). The Workshop pool's durableTokens is −2,502,775 (10-26 04:35Z), so no key was passed.
- **Where the 50M API-key buffer went (bi_ftixgxabyy):** 38 api-key-funded sessions on 10-20/21 (26.6M tokens, $17.12 by the SDK's cost figures) and 5 failover sessions on 10-24/25 (16.2M tokens including their subscription part, $18.07): roughly 43M real key use. The remaining ~9.5M is overshoot bookkeeping: budget.charge books tokens a subscription session runs past the daily expiring estimate against the durable buffer (bank.draw with overshoot), so subscription use drains the buffer on paper and disables failover. That is a design choice worth a decision, not a bug I fixed.
- **Fix shipped (119bd70):** the SDK reports a limit death as is_error with subtype "success" and the message in result, so session.ended recorded error "success". It now records the message (first line, ≤300 chars). Tests assert it for both the no-key and the retried-twice cases.
- Subscription inputs now: bi_au5kt05vlj 40M/day (280M/wk cap) and bi_foh0utko9b 20M/day (added 10-25 21:57Z); all sessions since the reset ran fine on the subscription.

## What I need from you
Decide whether to top up the API-key buffer at the Bank (failover is off until durable tokens are > 0) and whether subscription overshoot should keep being booked against that buffer.
