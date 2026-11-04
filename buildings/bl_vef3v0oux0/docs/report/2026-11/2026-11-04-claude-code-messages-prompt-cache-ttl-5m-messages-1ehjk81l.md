---
id: "dc_sn1ehjk81l"
type: "report"
state: "building"
title: "CLAUDE_CODE_MESSAGES_PROMPT_CACHE_TTL=5m: messages 5m, system prompt stays 1 h, so warm wakes are kept"
authorId: "ag_s5xpo2tdtm"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Read-only answer, done. The lever (CLAUDE_CODE_MESSAGES_PROMPT_CACHE_TTL=5m on runtime and desk sessions: messages 5m, system prompt and tools stay 1 h, warm wake kept) goes to Mitchell as a Needs item in the next rollup; it is a token-accounting change, so it is his to decide."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-04T19:09:00.792Z"
sessionId: "se_0had8uqtav"
assignmentId: "as_z6vm9idttd"
costUsd: 0.7594774
tokens: 37974
turns: 15
createdAt: "2026-11-04T19:08:23.590Z"
updatedAt: "2026-11-04T19:09:00.792Z"
---
## What I did
I read the installed Claude Code CLI 2.1.316 bundle (`/opt/agent-town/node_modules/@anthropic-ai/claude-agent-sdk-linux-x64/claude`): the env and settings schema, `psn`, `PTe` and `Eee`, and the request builder that sets the cache markers. This was read-only: no env was set, nothing was run, no PR. Topic page [dc_wcfoeo59bn](../../wiki/2026-11/2026-11-04-cache-ttl-why-every-cache-write-is-1-h-since-2026-foeo59bn.md) now has the lever paragraph.

## Findings
| | `CLAUDE_CODE_MESSAGES_PROMPT_CACHE_TTL` | `CLAUDE_CODE_PROMPT_CACHE_TTL` |
|---|---|---|
| (1) What it affects | **Message cache markers only**: `Tw = Eee(IW)`, passed to `YSr(...,Tw,...)`. The tools and system prompt keep `IW` from `PTe`, via `ZSr(...,{cacheTtl:IW})`. | **The whole main-thread request** (tools, system and messages). "Main thread" means sources matching `I9e = [repl_main_thread*, sdk, auto_mode, memdir_relevance]`. Subagents and helpers use `CLAUDE_CODE_SUBAGENT_PROMPT_CACHE_TTL`. |
| (2) Accepted values | Only exactly `"5m"` has an effect (`Eee`: `==="5m"?"5m":e`). It can only lower a TTL, never raise one. | `"5m"` or `"1h"`. The builder sends `ttl:"1h"` only when the value is "1h"; anything else means the API default of 5m. |
| (3) Interaction with the 1 h allowlist and funding | None. It is a post-filter applied after `PTe`, so it applies whatever the funding or flags. | It overrides them. `psn` returns it before the checks for subscription, overage, `tengu_prompt_cache_1h_config` and `tengu_tidy_frost`. Only `FORCE_PROMPT_CACHING_5M` comes before it. Settings `promptCacheTtl` and `subagentPromptCacheTtl` rank below the env vars. |
| (4) Warm manager wake (−42%, [dc_qgl1lbe7wm](../../wiki/2026-11/2026-11-03-prompt-caching-fix-85498fa-measured-live-l1lbe7wm.md)) | **Kept.** The tools and system-prompt prefix stay 1 h, so the next wake within 60 min reads them. The first message becomes 5m, but each wake has its own first message, so it was never read across wakes. The cost: a pause of more than 5 min inside one session re-writes the messages (the system prompt is still read). | **Lost.** The prefix becomes 5m, so a wake 5–60 min later is cold. |

Code locations (byte offsets in the binary, the source copy): `PTe` and `tengu_tidy_frost` at about 285,832,763. `psn`, `Eee` and `I9e` at about 285,257,400. The request builder (`IW`, `Tw`, `ZSr`, `YSr`) at about 285,871,100. The settings descriptions (`promptCacheTtl`) at 274,311,491.

Inferred: setting `CLAUDE_CODE_MESSAGES_PROMPT_CACHE_TTL=5m` in the session env of runtime and desk is the lever that does what tidy_frost did, minus its 1 h first-message write. That is roughly the $27–29/day list-price Fable saving in [dc_wcfoeo59bn](../../wiki/2026-11/2026-11-04-cache-ttl-why-every-cache-write-is-1-h-since-2026-foeo59bn.md), and about $10/day on Opus. Not verified: whether the API bills a mixed 1 h/5m request the way the code intends. The first session after any change would show it in `usage.cache_creation`.

## What I need from you
Nothing needed. This is the input to the manager's Needs line for Mitchell: whether to set `CLAUDE_CODE_MESSAGES_PROMPT_CACHE_TTL=5m` on runtime and desk sessions.
