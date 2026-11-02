---
id: "dc_hlhvzz3ic3"
type: "report"
state: "building"
title: "One credential per session, enforced (audit + fix + daily reconciliation): PR #129 merged, main 6b162cd should be live next; desk image rebuild queued"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_bq7yfn5dr8","dc_32xbgegtvn"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/129","https://platform.claude.com/docs/en/manage-claude/usage-cost-api"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: audit + enforcement + daily reconciliation on main at 6b162cd (PR #129), fast check green. The proposal (verify live: boot, migration 062, first reconciliation event, HUD alert) is already running as the parked continuation as_0e4am4nw6y, which also files the rollup carrying the ANTHROPIC_ADMIN_KEY need; no second assignment. Not rolling up from this team-lead session so Mitchell gets one rollup with live evidence."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-31T00:06:59.660Z"
sessionId: "se_tynrh6qzs4"
assignmentId: "as_xdlppphh08"
costUsd: 12.081957199999998
tokens: 241639
turns: 64
createdAt: "2026-10-31T00:05:57.974Z"
updatedAt: "2026-10-31T00:06:59.660Z"
---
## What I did
Audited `packages/core/src/budget.ts`, `packages/runtime/src/sdk.ts`, the desk env builder (`packages/runtime/src/desk/session.ts`) and the desk itself (`packages/desk/src/run.ts`) for every session path, then enforced the invariant and added the daily check. PR #129 (52ae35a, merged with main as 12a67c1) → main **6b162cd**. `npm run check -- --fast` green before and after merging main. `redeploy image=true` queued (the desk image changed); 6b162cd should be live when this is read. Topic page [dc_32xbgegtvn](../../wiki/2026-10/2026-10-31-one-credential-per-session-and-the-daily-funding-r-xbgegtvn.md); Pix told (ms via tell).

## Findings
**Audit (before the change).** Host paths (work, manage, facilitate, chat, meeting summaries and replies) got exactly one credential: `sessionEnv` asserts the host env holds none and adds the Bank's one. Desk paths got **two**: `deskAuth` put the subscription token *and* the fallback key (`AGENT_TOWN_FALLBACK_API_KEY`) in the desk env; the desk stripped the key from the SDK env but reran the whole session on it after a spend-limit death, inside the same town session. The Bank then *rebooked* the session to the fallback allocation on the desk's word (`fundingUsed`/`fallback` at session end) and had no record of which input the session was actually handed. No test failed when a path passed two (the desk tests asserted the two-credential env on purpose). A desk that failed over and then crashed before session-end would have been booked to the subscription while the key paid: the post-mortem's shape again.

**Enforced (docs/invariants/bank.md 9 and 10, each with its tests).**
- `Funding` has no `fallback`. `assertOneCredential` runs on every env that leaves the host (host `sessionEnv`, desk `deskEnv`): exactly one of `CLAUDE_CODE_OAUTH_TOKEN` / `ANTHROPIC_API_KEY` / `ANTHROPIC_AUTH_TOKEN`, no fallback key beside it. Tests fail if any path passes two, none, or a key beside one.
- Failover is the next session's pick: a spend-limit death ends the session with `spendLimit` → `bank.cap`; while `Bank.capState().cappedAt` is set (a cap whose reset is still ahead) `Budget.fundingFor` hands subscription-funded sessions `failoverFunding` (a donor-key allocation's key, else the api-key input's own) and books them to it. The desk never reruns on another key; a fallback key from an old runtime is dropped.
- The Bank books what it handed out: `sessions.credentialInputId` (migration 062, nullable, additive) + `funding` are written at start from the same `Funding` the env was built from. A desk's differing claim (or an old image's `fallback: true`) appends `alert: funding-mismatch`; the booking never changes.
- Daily reconciliation: `reconcileDue` (runtime tick, once per UTC day for the day before) → `reconcileFunding` (core `reconcile.ts`): api-key sessions on unlisted inputs, mismatches, and, with the collective secret `ANTHROPIC_ADMIN_KEY`, the Console's cost report (`GET /v1/organizations/cost_report`, raw HTTP, amounts in cents) against the Bank's api-key spend, tolerance max($1, 10%). One `system` event per day; `alert: funding-reconcile` when unexplained. The HUD shows funding alerts (`fundingAlert`) for a day.

**Behaviour change to know.** A session that hits the subscription cap now ends with the usual "ended without a report" fallback report in my in-tray instead of silently rerunning on the key; `continue` re-runs it, and that run picks the key. Automatic re-queue is not built.

**Checks.** 6 test files changed or added (core `reconcile.test.ts` 4, runtime `reconcile.test.ts` 2, `secrets.test.ts`, `desk.test.ts`, `bank-fallback.test.ts`, desk `run.test.ts`); fast check green (docs, typecheck, core/runtime/desk suites, 21 web files / 105 tests). Not verified yet: the live boot at 6b162cd (migration 062 applied, the first "Bank reconciliation for 2026-10-30" event after the next tick); that is the parked continuation.

## What I need from you
Add the org's Admin API key (`sk-ant-admin…`) as the collective secret `ANTHROPIC_ADMIN_KEY` at Town Hall → Secrets so the daily reconciliation reads the Console; until then the daily event says "Console not checked".
