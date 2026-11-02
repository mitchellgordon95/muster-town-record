---
id: "dc_5h4qaxiqjh"
type: "report"
state: "building"
title: "Bank Transparency: \"Not funded\" grant closed as done, the Spending row now explains itself (PRs #188, #196, #208 live at f51fa0f); three key results to mark met, one missed; recurring key donations limited to N credits and API-key-only hosted collectives also live"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_3cuhr9j0we","dc_vurxxsq1tu","dc_ltb8hesjzj","dc_sj1xnmn9v2","dc_opfj4qqyle","dc_i6y3odvbj6","dc_hr5pjg04xn","dc_nzjrxs1zf2","dc_fuyoi9k2ty","dc_3e1iakhlrq","dc_uvbcl8tod6"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/208","https://github.com/mitchellgordon95/muster-town/pull/216","https://github.com/mitchellgordon95/muster-town/pull/202","https://github.com/mitchellgordon95/muster-town/pull/221"]}
tags: ["rollup","checkpoint","parked"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-11-01T00:47:34.141Z"
sessionId: "se_8djvl30tkk"
assignmentId: "as_yulscv4bbv"
costUsd: 4.2662476499999995
tokens: 85325
turns: 21
createdAt: "2026-10-31T22:36:25.590Z"
updatedAt: "2026-11-01T00:47:34.141Z"
---
Live f51fa0f since 22:30 UTC (carries PRs #206, #208, #216; #202 and #196 earlier). This is the close report for gr_wp2rg302qu: it crossed its 100% checkpoint while its last step ran, so I verified the key results live myself and closed it as done rather than hold it (366,224 of 300,000 tokens spent, nothing to return; the step 3 fork was still finishing, its report is on its way to my in-tray).

## Shipped

**1. The Bank's "Not funded" row explains itself**
**What it is:** The Spending tab's "Not funded" row (195,957 adj. tokens) now carries a note that says what it is (usage the Bank never debited), why (before PR #131 the runtime skipped the debit for some sessions; that is fixed), when it stopped (no unpaid usage since 2026-10-26), which buildings (Onboarding 535,569, Prod 123,238, by usage row), why the by-building rows come to more than the row (Not funded is a net total, the split counts each undebited row in full) and that it is written off. The number itself has not moved since 10-29. PRs #188, #196, #208 (gr_wp2rg302qu; plan [dc_3cuhr9j0we](2026-10-31-gr-wp2rg302qu-not-funded-row-explains-itself-cut-i-uhr9j0we.md), rule [dc_cvp89lj91o](2026-10-28-not-funded-row-split-live-in-code-weightmismatch-c-p89lj91o.md), findings [dc_8qozlz0wsb](../../note/2026-10/2026-10-31-findings-the-bank-s-not-funded-row-has-stopped-gro-ozlz0wsb.md)). A one-line follow-up, PR #221, adds "recorded but not charged. Fixed on 2026-10-31" to the Why line; it merges when CI is green.
**What you'd see:** muster.town → "$" → Bank → Spending, signed out: expand "Not funded: work sessions the Bank never charged −195,957". GET /api/finance/spend at 22:31 UTC: notFunded 195,957, notFundedLastAt 2026-10-26T22:52Z, split 658,807 with a reason, check ok.
![The Not funded row's note, signed out at f51fa0f](/api/media/mf_s5y1xy1red)
**Your call:** Mark three key results met and one missed: kr_518ed152d2 "the split adds up exactly" cannot hold, because the row is a net total and the split is a per-row estimate; the page says so instead of hiding it. If you would rather the split be forced to equal the row, say so and I will propose it.

**2. Recurring API-key donations limited to a number of credits**
**What it is:** A recurring Bank input from a pasted API key can now be set to run N times instead of until cancelled: the Donate form asks "For how long", the input stops by itself after the last credit and stays listed, and the daily-inflow projection counts only the credits still due. Migration 074 adds two nullable columns (additive). PR #216, merged f51fa0f ([dc_fuyoi9k2ty](2026-10-31-recurring-api-key-donations-limited-to-n-credits-p-yoi9k2ty.md), [dc_3e1iakhlrq](2026-10-31-pr-216-had-a-conflict-with-main-docs-log-md-so-ci-1iakhlrq.md), [dc_uvbcl8tod6](2026-10-31-pr-216-merged-as-f51fa0f-redeploy-queued-live-pict-bcl8tod6.md)). Your ask from our 1:1 ([dc_dw0izucnip](../../meeting-notes/2026-10/2026-10-31-1-1-mitchell-and-nell-notes-0izucnip.md)).
**What you'd see:** Signed in, Bank → Donate, Source: API key, daily: "For how long: A number of times", "Times (the first credit is now)" 3, total line "3 × 1,000,000 = 3,000,000 adj. tokens over 3 days". Live inflow unchanged at 11,500,000/day (no limited input exists yet); check:finance all 15 ✓ at f51fa0f.
![Donate form with "A number of times" selected, live at f51fa0f](/api/media/mf_u74ki6w79c)
**Your call:** Bank change you asked for yourself; nothing to decide unless the form's wording should change.

**3. Hosted collectives run on an API key only**
**What it is:** A hosted collective's Bank refuses a subscription input, its credential chooser never returns a subscription (a stray row is inert), and no hosted session's environment carries an OAuth token. PR #202, live ([dc_nzjrxs1zf2](2026-10-31-hosted-collectives-api-key-only-pr-202-open-waitin-jrxs1zf2.md)). Your ask from the same 1:1. API and credential level only, no picture.
**What you'd see:** A hosted collective with no key shows "A hosted collective runs on an Anthropic API key only; add one at the Bank" instead of the subscription hint; its Donate form offers no subscription source.
**Your call:** Bank/credential change you asked for yourself; none.

## Decided
- [dc_3cuhr9j0we](2026-10-31-gr-wp2rg302qu-not-funded-row-explains-itself-cut-i-uhr9j0we.md) (plan: Not funded split, note, live check) → approve
- [dc_vurxxsq1tu](2026-10-31-not-funded-step-1-get-api-finance-spend-now-splits-rxxsq1tu.md) (step 1, PR #188 built) → approve
- [dc_ltb8hesjzj](2026-10-31-not-funded-step-2-spending-note-explains-cause-sto-b8hesjzj.md) (step 1, PR #188 merged 88cce35) → approve
- [dc_sj1xnmn9v2](2026-10-31-checkpoint-for-gr-wp2rg302qu-not-funded-row-explai-1xnmn9v2.md) (first checkpoint moot: you raised the grant to 300k) → approve
- [dc_opfj4qqyle](2026-10-31-not-funded-step-2b-split-nets-donation-paid-usage-fj4qqyle.md) (step 2, PR #196 the note) → approve
- [dc_i6y3odvbj6](2026-10-31-pr-208-ci-was-red-only-from-main-s-old-finance-fly-y3odvbj6.md) (step 2b, PR #208 built) → approve
- [dc_hr5pjg04xn](2026-10-31-pr-208-merged-as-b9e1e5a-redeploy-queued-step-3-do-5pjg04xn.md) (step 2b, PR #208 merged b9e1e5a) → approve
- [dc_nzjrxs1zf2](2026-10-31-hosted-collectives-api-key-only-pr-202-open-waitin-jrxs1zf2.md) (hosted collectives API-key only, PR #202) → approve
- [dc_fuyoi9k2ty](2026-10-31-recurring-api-key-donations-limited-to-n-credits-p-yoi9k2ty.md), [dc_3e1iakhlrq](2026-10-31-pr-216-had-a-conflict-with-main-docs-log-md-so-ci-1iakhlrq.md), [dc_uvbcl8tod6](2026-10-31-pr-216-merged-as-f51fa0f-redeploy-queued-live-pict-bcl8tod6.md) (recurring donations limited to N credits, PR #216) → approve
- Step 3's live-check report (as_0q37kh9x7c) and the Donate-picture report (as_1vtz85ct8n) land after this: approve, nothing else.

## Key results
gr_wp2rg302qu "Not funded row explains itself": closed as done, 366,224 / 300,000 (crossed 100% at 303,962 while step 3 ran).

| Key result | Status | How to check | What the check showed (f51fa0f, 22:31 UTC) |
|---|---|---|---|
| kr_jksobb0bwo no work session goes unpaid; the note says the cause and the write-off | claimed | notFunded equal two days running after the fix; no unpaid usage row after the fix date; the note names the cause | 195,957 at every read: 10-29 03:48Z, 10-30 02:15Z, 10-31 20:49Z, 22:29Z, 22:31Z. notFundedLastAt 2026-10-26T22:52Z; the fix (PR #131) merged 2026-10-31 00:36Z. The endpoint applies the 2-second rule of [dc_cvp89lj91o](2026-10-28-not-funded-row-split-live-in-code-weightmismatch-c-p89lj91o.md); the SQL itself was not run (no DB access from a desk). Note names PR #131 chargeUsage and says written off. |
| kr_518ed152d2 the by-building split adds up to notFunded exactly | claimed, **not met** | sum of notFundedSplit = notFunded; a core test passes | Split 658,807 ≠ 195,957 (ok false, reason shown). The core test covers both the equal case and the unequal case with the reason. Mark missed. |
| kr_b8a2c4118e the note gives the cause, the stop date and the write-off in plain words | claimed | expand the row signed out; a web test asserts it | Live note: "work sessions the Bank never charged", "before PR #131 (chargeUsage) the runtime skipped the debit", "No new unpaid usage since 2026-10-26", Onboarding and Prod with tokens and usage rows, "Written off: not charged to any building". Web test finance.test.tsx asserts the lines. PR #221 (CI) adds "recorded but not charged. Fixed on 2026-10-31". |
| kr_1fb47352c8 the row stopped growing | claimed | notFunded 195,957 on the live-check day and the day before | 195,957 on 10-29, 10-30 and 10-31. The daily schedule sc_qu4lpdmgng re-reads it on 11-01 and 11-02 at 03:00 UTC. |

gr_rdzg83m0al "runway counts inflow": closed as done in the last rollup ([dc_veanch9dvs](2026-10-31-bank-transparency-grant-closed-as-done-the-bank-s-anch9dvs.md)), 227,060 / 160,000, four key results claimed, your marks pending there.

Today's spend by lane: exploration 68,592 tokens (free under the goal: 36,220); directed 1,232,478 tokens.

## Needs from Mitchell
Nothing needed beyond marking the four key results above from this report: three met, kr_518ed152d2 missed.

_Already waiting in your in-tray: 0 proposals, 0 requests, 1 rollup ([dc_veanch9dvs](2026-10-31-bank-transparency-grant-closed-as-done-the-bank-s-anch9dvs.md))._
