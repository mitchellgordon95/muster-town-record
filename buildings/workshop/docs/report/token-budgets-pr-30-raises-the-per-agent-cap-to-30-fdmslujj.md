---
id: "dc_1yfdmslujj"
type: "report"
state: "building"
title: "Token budgets: PR #30 raises the per-agent cap to 30M, PR #32 adds a building daily pool, design doc on the board"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "there should be a way to configure the building token budget when you make the building and also via like some building settings"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T04:24:43.956Z"
sessionId: "se_5z4hv9ikkq"
assignmentId: "as_lz85koovyr"
costUsd: 1.3797483999999998
tokens: 2446490
turns: 42
createdAt: "2026-10-20T04:22:58.021Z"
updatedAt: "2026-10-20T04:24:43.956Z"
---
## What I did
- Read the budget code (`packages/core/src/budget.ts`, `runtime/session.ts`, `seed.ts`).
- Opened two draft PRs and wrote a design doc on the Workshop board: "Design: token budgets today, and the waterfall" (dc_pxkzsigtgh).
- Fixed a migration-number clash in my own PR #27.

## Findings
- **How budgets work today:** each building has one lifetime pot made of its donations. It never refills. Each agent has a fixed daily cap (`dailyTokensPerAgent`), checked only when a session starts and charged after it ends. There is no daily limit for the building as a whole and no town treasury: the `town.allocate_budget` permission exists but nothing uses it. So it isn't a waterfall yet.
- **Other gaps the doc lists:**
  - A session can overshoot a cap by up to about one session per running agent.
  - Each charge lands on a single allocation, even when that allocation has less left than the charge. The excess is never taken from the next allocation, so the building looks like it has more left than it does.
  - When a building has 0 left, spend is recorded on the agent but on no allocation.
- **PR #30** (https://github.com/mitchellgordon95/agent-town/pull/30):
  - Raises the default per-agent cap from 10M to 30M tokens a day.
  - On restart, seed raises any building still on exactly 10M to 30M; custom values are left alone.
  - Raising a cap now resumes residents who ran out today, instead of waiting until midnight. Root was out of budget today and would get going again.
  - Typecheck clean; `npm test` 168/168, including 3 new tests.
- **PR #32** (https://github.com/mitchellgordon95/agent-town/pull/32), stacked on #30:
  - Adds an optional building daily pool (`dailyTokens`, migration 011). Agents draw from it as they work, each up to the per-agent max.
  - When the pool runs out, residents park until midnight or until the pool is raised or cleared.
  - The pool is a field in Settings and a meter row in the building panel. `/api/budget` reports `dailyTokens` and `spentTodayTokens`, so Pix's #31 cards can show them.
  - With no value set, behaviour is unchanged.
  - Typecheck clean; `npm test` 170/170. I haven't checked the UI in a browser.
- **Migration clash:** #27 and Pix's #28 both added a migration numbered `009`. The migration runner applies only one file per number, so one of the two would silently never run. I renumbered #27's to `010`; typecheck and all tests still pass on that branch.
- **Still to build:** fixing the charge bookkeeping, then the town treasury (`POST /api/budget/allocate`). These are steps 3 and 4 in the doc, for my next session.

## What I need from you
Merge #30 and then #32, and decide the daily pool size for buildings: I suggest no limit by default, with the Workshop set to about 60M tokens a day.

## Reply from Mitchell (2026-10-20 00:24)

there should be a way to configure the building token budget when you make the building and also via like some building settings

