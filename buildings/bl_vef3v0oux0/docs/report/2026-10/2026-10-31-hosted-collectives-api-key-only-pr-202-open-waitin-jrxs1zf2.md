---
id: "dc_nzjrxs1zf2"
type: "report"
state: "building"
title: "Hosted collectives API-key only: PR #202 open, waiting on CI"
authorId: "ag_5dmm2fckm3"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged: PR #202 is built and its merge-on-green continuation is already parked as as_dt1nfqsh8j (waitFor pr 202), so no new assignment. Goes into the next rollup as a directed item with a \"Your call\" line once its merge is live."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-31T21:26:18.388Z"
sessionId: "se_et2dootv4n"
assignmentId: "as_yv75rc0svj"
createdAt: "2026-10-31T21:20:59.908Z"
updatedAt: "2026-10-31T21:26:18.388Z"
---
## What I did
Built Mitchell's ask from 1:1 mt_p3ge56kg03 as one PR: https://github.com/mitchellgordon95/muster-town/pull/202 (branch agent/nell-1/hosted-collectives-never-run-on-a-subscr, commit on top of main e8bd323). `npm run check` passed locally (docs, deadcode, typecheck, all tests). Now waiting on CI.

## Findings
- **Core** (`bank.ts`, `budget.ts`, `permissions.ts`): `Permissions.isHosted()` / `Bank.hosted()` read `world.host.hosted`. In a hosted World:
  - `Bank.addInput` refuses a subscription input.
  - `subscriptionCredential()` returns null even when a stray subscription row exists.
  - `townCredential()` throws `NoCredential(HOSTED_KEY_ONLY_HOLD)` = "A hosted collective runs on an Anthropic API key only; add one at the Bank".
  - `Budget.fundingFor` now wraps the old body (renamed `pickFunding`). Wherever a subscription would have paid, it uses the Bank's API key if there is one, otherwise it throws that hold. A final check throws on any subscription result, which covers the failover paths too.
  - The Workshop is unchanged.
- **Runtime**: `assertHostedCredential` runs in `sessionEnv` (host sessions via `townOptions`, and `oneShot` for meeting summaries) and in `deskEnv`. Each refuses to put `CLAUDE_CODE_OAUTH_TOKEN` into a hosted session's env. A hosted runtime already got `hostedEnv`, which has no host credentials, so no session falls back to a token from the host env.
- **Web**: Donate (`BankFunding.tsx`) treats a collective as hosted when its health reports a `funding` or the app is served under `/<slug>/`. There it offers no subscription source, and a stale "subscription" pick is coerced to api-key. The API errors at routes/town.ts:330/:397 are kept. There is no separate Town Hall inputs form: `addBankInput` is only called from this form.
- **Visible change**: a hosted collective with no key now shows the hosted hold message instead of NO_KEY_HOLD ("add your Claude subscription token or…"). The existing runtime test was updated to match.
- **Tests**:
  - core `bank.test.ts`: a stray subscription refuses and says to add a key; with a key it runs on the key; the Workshop still runs on its subscription.
  - runtime `hosted.test.ts`: a stray subscription is held and nothing reaches the SDK; with a key beside it, the env carries no OAuth token.
  - runtime `secrets.test.ts`.
  - web `hostedDonate.test.tsx`.
- **Docs**: a paragraph in `docs/hosted-collectives.md` says why (Anthropic's subscription terms).
- **No migration**: a stray row is now inert, so nothing needs cancelling.

**Plan for the continuation:**
1. When CI on #202 is green, merge it and call `redeploy`.
2. Next session, check the deploy is live (`git merge-base --is-ancestor <merge sha> <health commit>`), then confirm `GET /<slug>/api/town` on a hosted slug reports `health.funding` as `api-key` or `none`.
3. Rewrite topic page [dc_32xbgegtvn](../../wiki/2026-10/2026-10-31-one-credential-per-session-and-the-daily-funding-r-xbgegtvn.md) and add a log line.
4. Rollup "Your call": this is a Bank/credential change that Mitchell asked for himself.

## What I need from you
Nothing needed.
