---
id: "dc_f0itukd3jq"
type: "report"
state: "building"
title: "gr_lwgus14rd2 step 2: cache-miss alert in PR #326, parked on CI; 20% threshold would fire for every purpose"
authorId: "ag_t9l7jema9p"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Keep CACHE_MISS_SHARE at 0.20 for the merge: the brief dc_g7q7s2vug8 (Mitchell's Claude Code session) says \"a fifth is a reasonable line\", and the live shares (30–85%) above it are the symptom the alert exists for, not noise. Whether to move the line is Mitchell's call; it goes in the next rollup's Needs. The 11-03 23:37Z flip to all-1-hour cache writes gets its own assignment (SDK dep is a caret range ^0.3.0 in packages/runtime/package.json:15, so a redeploy reinstall may have bumped it). as_pimtt2t8pf already merges #326 when CI finishes."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-04T18:54:59.564Z"
sessionId: "se_odtola3i8v"
assignmentId: "as_gc6u3sk0wf"
costUsd: 2.2822112999999993
tokens: 114111
turns: 52
createdAt: "2026-11-04T18:53:54.166Z"
updatedAt: "2026-11-04T18:54:59.564Z"
---
## What I did
Built the daily cache-miss check (kr_f49co6lg51) and opened draft PR https://github.com/mitchellgordon95/muster-town/pull/326. It is parked until CI finishes. I also replayed live session rows through the check to test the 20% threshold. I rewrote plan page [dc_qnpvanlfsb](../../wiki/2026-11/2026-11-04-token-cost-legible-gr-lwgus14rd2-plan-and-state-pvanlfsb.md).

## Findings
- **What it does.** The check lives in core `cache-miss.ts` and reuses step 1's `sessionKindUsd`, which is now exported. It looks at the UTC day's ended sessions, grouped by purpose × model, and raises an alert when either of two signals fires:
  - 1-hour cache writes are more than 20% of the group's list-price cost.
  - A session's first turn wrote more to the cache than it read.
- **Where the first-turn numbers come from.** Per-turn sizes are already stored: each session's transcript holds the first main-thread `assistant` record's `usage`. So no schema change was needed.
- **The event.** One `system` event per purpose per day, with payload `alert: "cache-miss"`, purpose, model, share, sessionIds (up to 10), firstTurn and day. Its text starts "Cache miss: …". The events log itself remembers what already fired today; there is no new table and no marker.
- **Runtime hook (for Pix: this is the shared tick).** One line beside the reconcile in `packages/runtime/src/index.ts` calls `cacheMissDue` from runtime `cache-miss.ts`. It only does work when a session has ended since its last run, and it memoizes first-turn reads per day.
- **HUD.** A "Cache alert" line, built like the funding alert, that opens Bank › Spending.
- **Checks run.** Tests cover 19% (no alert) vs 21% (alert), one alert per purpose, the first-turn rule, transcript parsing and the world events (core, runtime and web). Typecheck and the dead-code check are clean. 724 of 725 tests passed. The failure was `wakes-relay`, which is unrelated and passes when run alone.
- **Not proven live.** I did not do the clock-line breakage with a real wake, because a desk can't run a runtime wake without spending a credential. The unit tests are the proof for now.
- **Live data: the 20% threshold fires for every purpose, every day.** Replaying live session rows:

| Day | Purpose | 1-hour cache-write share of cost |
|---|---|---|
| 11-03 | manage | 34% |
| 11-03 | work | 30% |
| 11-03 | estimate | 49% |
| 11-04 | manage | 66% |
| 11-04 | work | 61% |
| 11-04 | facilitate | 57% |
| 11-04 | meeting-reply | 85% |
| 11-04 | estimate | 62% |

  Since the session that ended at 2026-11-03 23:37:19Z, every cache write is reported as 1-hour; the 5-minute share is 0% across about 178 sessions. That roughly doubled the 1-hour share. I found no cause in the repo, so it may be an SDK or provider change. Once deployed, expect a HUD cache alert every day for every purpose until the threshold changes.

## What I need from you
Decide whether to keep the 20% threshold (the alert will show every day) or set another value, such as 70%, before or after #326 merges.
