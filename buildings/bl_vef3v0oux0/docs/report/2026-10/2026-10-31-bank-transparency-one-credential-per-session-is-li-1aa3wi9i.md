---
id: "dc_wc1aa3wi9i"
type: "report"
state: "building"
title: "Bank Transparency: one credential per session is live at 6b162cd and verified (migration 062, first daily reconciliation event, HUD alert); one secret needed from you for the Console check"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_hlhvzz3ic3"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/129"]}
tags: ["rollup"]
verdict: "stop"
decision: "approve"
decisionNote: "in no universe does this project touch my or anyone else's anthropic console"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-31T01:06:07.325Z"
sessionId: "se_0b1ud3gebq"
assignmentId: "as_0e4am4nw6y"
costUsd: 3.1450641999999993
tokens: 62901
turns: 23
createdAt: "2026-10-31T00:10:56.004Z"
updatedAt: "2026-10-31T01:06:07.325Z"
---
Live commit 6b162cd (CI redeploy finished 2026-10-31 00:07:38Z; the desk image was pushed at 00:05Z and 26 idle desks were recreated from it).

## Shipped
**1. Every session runs on exactly one credential, the Bank books the one it handed out, and the Bank checks itself once a day**
**What it is:** The follow-up you asked for in the 1:1 with Pix after the post-mortem (dc_bq7yfn5dr8). Before, a desk left the host with the subscription token and a fallback API key and could switch to the key mid-session on its own word; the Bank then rebooked it on trust. Now an env that leaves the host carries one credential variable and no fallback key, and a test fails if any path (host work, manage, meetings, chat, summaries, desks) passes two or none. Failover happens between sessions, never inside one: while the subscription is capped, the next session is handed a donor key or the Bank's api-key input and booked to it. Each session row records the credential input it was handed (new nullable column, migration 062); a desk claiming something else only raises an alert, the booking never changes. Once a day the runtime reconciles the day before: api-key sessions on inputs the Bank doesn't list, desk claims that didn't match, and, once the collective has the org's Admin API key as a secret, the Console's cost report against the Bank's api-key spend. PR #129, build report [dc_hlhvzz3ic3](2026-10-31-one-credential-per-session-enforced-audit-fix-dail-hvzz3ic3.md), topic page [dc_32xbgegtvn](../../wiki/2026-10/2026-10-31-one-credential-per-session-and-the-daily-funding-r-xbgegtvn.md), invariants 9 and 10 in docs/invariants/bank.md.
**What you'd see:** API and runtime only, no picture. Verified live after the boot: every session started after 00:07:38Z shows a credential input on GET /api/sessions (bi_1oiloh5qwu, your "Max plan" subscription input of 23:31Z); sessions started earlier show null. The first reconciliation event fired 5 s after boot and reads: "Bank reconciliation for 2026-10-30: 164 sessions, Bank api-key $0.00, subscription $189.46, donor keys $0.00; no ANTHROPIC_ADMIN_KEY secret, Console not checked. OK" (nothing unlisted, no mismatches). When a day does not reconcile, the HUD shows a "Funding alert … Bank →" line for 24 h; the deployed bundle carries it, and today there is nothing to show because the day was clean.
**Your call:** A session that hits the subscription cap now ends with the normal "ended without a report" fallback report in my in-tray, where `continue` re-runs it on the key, instead of silently rerunning on the key inside the session. Automatic re-queue is not built; say if you want it.

## Decided
- [dc_hlhvzz3ic3](2026-10-31-one-credential-per-session-enforced-audit-fix-dail-hvzz3ic3.md) → approve (build report for PR #129; its parked continuation was this session, which verified live and files this rollup).

## Key results
| Key result | Status | Spent / granted |
|---|---|---|
| none funded (three open key results on the goal: kr_fydnpd8ok2, kr_zjawesqcyp, kr_jksobb0bwo; one proposal open) | — | — |

Today's spend by lane: exploration 0 / 1,000,000 tokens; directed: this verification session only (health showed 0 at 00:08Z, before it was booked). Queue: as_wwz0uvipwd (Donate-form ceiling line) pending; Nell 1 running as_l6dpiwsxzc (debit as the session runs, no lost usage on failure), both directed from the same 1:1.

## Needs from Mitchell
1. Add the org's Admin API key (`sk-ant-admin…`, from the Console's Admin keys page) as the collective secret `ANTHROPIC_ADMIN_KEY` at Town Hall → Secrets. Until then the daily reconciliation can only check the Bank against itself and says "Console not checked"; with it, a day whose Console bill exceeds the Bank's api-key spend by more than max($1, 10%) raises the HUD alert, which is the check that would have caught the 10-22 to 10-30 leak.

_Already waiting in your in-tray: 1 proposal (gr_8kg0kw4b64), 0 requests, 0 rollups._

## Reply from Mitchell (2026-10-31 01:06)

in no universe does this project touch my or anyone else's anthropic console

