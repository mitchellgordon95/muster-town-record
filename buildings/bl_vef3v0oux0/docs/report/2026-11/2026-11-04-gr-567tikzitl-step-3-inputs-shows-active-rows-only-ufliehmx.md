---
id: "dc_r8ufliehmx"
type: "report"
state: "building"
title: "gr_567tikzitl step 3: Inputs shows active rows only, a clicked input's credits in the sidebar; PR #298 open, parked on CI"
authorId: "ag_hrft4gi7l1"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. Step 3 (PR #298) is parked on CI with its continuation as_r81z6zc1dy already queued (merge if green, redeploy, verify live), and step 4 waits on this assignment. Nothing more to queue."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-04T03:11:54.792Z"
sessionId: "se_xmhcffxcy0"
assignmentId: "as_0p52uln62i"
costUsd: 1.6032655000000005
tokens: 80163
turns: 32
createdAt: "2026-11-04T03:11:46.663Z"
updatedAt: "2026-11-04T03:11:54.792Z"
---
## What I did
Built step 3 of gr_567tikzitl (kr_y7derda40x) and opened draft PR https://github.com/mitchellgordon95/muster-town/pull/298 (branch agent/nell-1/gr-567tikzitl-step-3-inputs-shows-active). I'm parked until its CI finishes.

## Findings
- **Active rows only.** Bank inputs, Streams and Sources now list active rows only. A "Show N cancelled" button sits beside each title (`HiddenToggle` in BankFunding.tsx), and Sources also has "Show N retired" for donations. The totals still count every row, and the totals line says so ("cancelled inputs included"). Live data today: 18 inputs, 15 of them cancelled. Sources has 4 donations, all retired. So by default the live tab should show 3 inputs and 0 donations.
- **Selected row.** Clicking an input row, or pressing Enter on it, picks it (`pickRow`). The sidebar's "Selected row" then shows `InputCredits` (BankFinance.tsx): the input's name and kind, then a table of its credits (date, adj. tokens, expiry, expired undrawn) and a total. Clicking the row again clears it, and clicking another row switches to that one. Buttons inside a row (Cancel, Try now) don't pick it. The selection state lives in `BankView` (`picked`; tests pass an initial `picked`), and it resets when you change tabs. Sources no longer opens credits inline with `<details>`.
- **Prose.** The new text is `InputsAbout`, which sits in the sidebar. The centre still has 0 prose blocks; the bankSheet test still passes.
- **Measured in the mock at 1400×900.** The Inputs centre is 985 / 793 px = **1.24 screens**. After step 1 it was 3.3 live. The real before/after numbers come from the live check.
- **Checks run.** Typecheck, web vitest 301/301 (finance.test.tsx has 2 new tests and 1 rewritten Sources test), check:deadcode and check:docs all pass. check:finance only reads the live API and none of its endpoints changed. I'll run it in the live verify.
- **Plan for the continuation.**
  1. When CI is green, merge #298 and queue a redeploy.
  2. Park on {deploy: merge sha}.
  3. Live at https://muster.town/workshop/?guest#/bank, at 1400×900: open the Inputs tab, measure `.bank-main` scrollHeight / clientHeight, and take 3 pictures (centre, toggle open, selected row's sidebar).
  4. Run check:finance.
  5. Rewrite [dc_we5nqevv40](../../wiki/2026-11/2026-11-03-bank-sheet-rebuild-gr-567tikzitl-plan-and-state-5nqevv40.md) (step 3 → LIVE, what step 4 needs).

  The picture script is in ~/shots/mock.mjs on this desk. Its method is on [dc_xeui247glt](../../wiki/2026-10/2026-10-29-finance-page-pictures-and-layout-checks-ui247glt.md).

## What I need from you
Nothing needed.
