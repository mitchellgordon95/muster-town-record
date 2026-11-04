---
id: "dc_57q5sn1oew"
type: "report"
state: "building"
title: "Why every cache write is 1 h since 11-03 23:37Z: Claude Code's remote flag changed, not our SDK or our counting"
authorId: "ag_2pcjf8w5ji"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_f0itukd3jq","dc_qgl1lbe7wm","dc_wcfoeo59bn","dc_qnpvanlfsb"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Good diagnosis: the 1 h writes are the CLI's subscriber default once tengu_tidy_frost went off; nothing in our code to fix. The TTL-env decision (cost behaviour, touches packages/desk) goes to Mitchell in the next rollup's Needs together with the 0.20 cache-alert line question."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-04T19:04:38.753Z"
sessionId: "se_ue4xo0px5q"
assignmentId: "as_4wef9mc9q9"
costUsd: 2.1442554
tokens: 107213
turns: 49
createdAt: "2026-11-04T19:04:17.234Z"
updatedAt: "2026-11-04T19:04:38.753Z"
---
## What I did
- Compared the API's own per-turn usage in 30 desk transcripts (11-01 → 11-04) with the town's session rows, split by model, before and after 23:37Z.
- Read how Claude Code CLI 2.1.316 picks the cache TTL (the `PTe` function), the cached remote flags on this desk, and the SDK lockfile.
- Wrote the topic page [dc_wcfoeo59bn](../../wiki/2026-11/2026-11-04-cache-ttl-why-every-cache-write-is-1-h-since-2026-foeo59bn.md) and updated the step-2 note on the plan page [dc_qnpvanlfsb](../../wiki/2026-11/2026-11-04-token-cost-legible-gr-lwgus14rd2-plan-and-state-pvanlfsb.md).
- No PR: there is nothing in our code to fix.

## Findings
**What the transcripts, rows and CLI show:**
- **The 1 h writes are real billing, not a counting error.**
  - Every desk transcript reports 5m = 0 on every turn, from 11-01 to now, both before and after 23:37Z (CLI 2.1.316, Opus 5.5).
  - Two rows checked against their transcripts match exactly: se_z96r7va18n has 58,200 1 h in both, and se_ppa0jsqzwh has 92,765 in both.
  - So `sdkTokenCounts` (tokens.ts) counts correctly.
- **Only Fable 5.1 changed.**
  - From 11-02 20:41Z to 11-03 23:37Z, Fable manage sessions were 53% 5m and Fable work sessions 58% 5m. Since then both are 0% (143 manage + 30 work sessions).
  - Opus 5.5 was 100% 1 h in both periods.
  - No session ended between 23:37:19Z and 00:00:41Z, so the switch happened inside that gap.
- **The CLI picks the TTL itself.** Its own help text: "Unset = automatic: 1 hour on a Claude subscription within its usage limits, 5 minutes on an API key". In `PTe`:
  - Env and settings come first: `CLAUDE_CODE_PROMPT_CACHE_TTL`, the `promptCacheTtl` setting, `ENABLE_PROMPT_CACHING_1H`.
  - With none set, a subscriber gets 1 h, under the remote allowlist `tengu_prompt_cache_1h_config` (which includes `sdk`).
  - The one exception: remote flag `tengu_tidy_frost` is on and the last main-thread request is under 5 min old. Then the TTL is 5m ("live_5m_cache").
  - All our sessions are `funding: subscription`.
- **The flag is off now.** This desk's flag cache (`~/.claude.json` plus 5 backups, 11-04 03:05Z → 18:55Z) has no `tengu_tidy_frost` key.
- **The SDK did not change.** The lockfile pins 0.3.304 for both runtime and desk, unchanged since 11-01 (0de09940). No runtime, desk or tokens.ts commit landed on main between 22:23Z and 00:22Z. Pinning the SDK would change nothing.

**What I infer:**
- `tengu_tidy_frost` was on for our Fable sessions from about 11-01 until about 23:40Z on 11-03. While it was on, a session's first request wrote 1 h and later turns wrote 5m. Turning it off (remotely) put every write back on the CLI's subscriber default of 1 h.
- So the 20% cache-alert line in PR #326 will be crossed every day by design, not because of a cache bug.
- **Cost at list price** (shadow dollars: the town pays a subscription, not per token):
  - Fable 1 h writes cost $20/M against $12.50/M for 5m.
  - 11-04 00:00–19:00Z rows have 5.29M Fable 1 h write tokens. Writing turns at 1 h instead of 5m therefore costs about **$27–29/day**.
  - Opus is unchanged; at 5m it would cost about $10/day less.
  - On a subscription, the real effect is on usage limits, not cash.

**What I don't know:**
- Why the flag was on, and whether it targeted Fable only.
- The exact flip time inside the 23:37–00:00Z gap.
- Whether `CLAUDE_CODE_MESSAGES_PROMPT_CACHE_TTL=5m` (the variable exists in the CLI) would make turns 5m while keeping the system prompt at 1 h.
- My session list may miss agents whose sessions all ended before 15:57Z today, so the $/day is a lower bound. Its 1 h total (10.2M) is in line with Bank › Spending today (8.85M).

**Lever, not shipped:** set a TTL env in the session env (runtime and desk `sdk.ts`). `CLAUDE_CODE_PROMPT_CACHE_TTL=5m` would also make each session's first write 5m. That gives up warm manager wakes, which were −42% adjusted tokens per wake ([dc_qgl1lbe7wm](../../wiki/2026-11/2026-11-03-prompt-caching-fix-85498fa-measured-live-l1lbe7wm.md)). It changes cost behaviour and touches packages/desk, so it needs Mitchell's call.

## What I need from you
Decide whether to keep the CLI's 1 h default (and move or redefine the 0.20 cache-alert line), or have a session try `CLAUDE_CODE_MESSAGES_PROMPT_CACHE_TTL=5m` on runtime and desk sessions to get back about $27/day at list price.
