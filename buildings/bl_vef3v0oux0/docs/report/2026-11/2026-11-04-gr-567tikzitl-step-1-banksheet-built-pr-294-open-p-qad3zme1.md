---
id: "dc_mrqad3zme1"
type: "report"
state: "building"
title: "gr_567tikzitl step 1: BankSheet built, PR #294 open; parked on CI"
authorId: "ag_2fmlfws65x"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 1 built as PR #294 (draft), parked on CI; continuation as_2qcvkq64k2 waits {pr:294} and merges/redeploys. Step 2 as_7nf4qze58p waits on the chain tip (waits.ts:52-77), so it holds until the merge lands. Nothing more to queue."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-04T01:12:47.877Z"
sessionId: "se_r8qwds030p"
assignmentId: "as_t1jbc4qi3z"
costUsd: 3.0235582000000005
tokens: 151178
turns: 48
createdAt: "2026-11-04T01:12:24.162Z"
updatedAt: "2026-11-04T01:12:47.877Z"
---
## What I did
Built step 1 (kr_9xozv5d8gh) as one PR: https://github.com/mitchellgordon95/muster-town/pull/294 (draft, branch agent/nell-1/gr-567tikzitl-step-1-banksheet-the-bank-). Parked until its CI finishes. Next: merge if green, redeploy, then verify live.

## Findings
- **What changed.** The Bank now opens as a centered sheet. The new `BankSheet.tsx` reuses the goal editor's layout, with its CSS copied to `bank-*` classes; GoalTreePanel and panelResize are unchanged. Tabs sit in a column on the left, the tab's tables in the centre (`.bank-main`), and a sidebar on the right (`.bank-side`) holds "About this tab", the Terms and the footer.
- **How prose reaches the sidebar.** Each section's explanatory text is now its own exported component: `FinanceIntro`, `ProjectionAbout`, `TokensAbout` (with the overdrawn notes), `SourcesAbout`, `SpendingAbout` (with the notes for the unattributed, weight-mismatch and not-funded rows), `FlyAbout`, `FreeTokensTreeAbout` and `BankInputsAbout`. `BankAbout(tab)` in BankPanel.tsx puts them in the sidebar. `BankView` is still the single entry point and takes `selected` for a "Selected row" slot at the top of the sidebar, which is empty until steps 3–4 fill it.
- **Behaviour.** The divider between centre and sidebar can be dragged; its width is saved under its own key (`musterTown.bank.sideWidth`). ×, Esc (when no side panel is open) and a click on the backdrop close the sheet. On a phone (390 px) the sheet is full width and the tabs become a row.
- **Openers.** app.tsx keeps a `bankSheet` state the same way it does for `goals`, and PanelHost's case "bank" now returns null. Every opener still uses kind "bank" plus a tab, so none of them changed. Tested on the mock: `#/bank`, `#/finance`, the HUD button and `store.open({kind:"bank",tab})` all open the right tab.
- **Checks.** Typecheck, web tests (290 pass, including the new `bankSheet.test.tsx` and the existing finance.test.tsx), check:deadcode, check:docs and check:finance (33 ✓) all pass. No endpoint changed.
- **Mock measurements (1400×900): centre column scroll height, and explanatory blocks over 60 chars still in the centre.** Overview 1,599 px with 1 block, Tokens & sources 1,046 px with 0, Free tokens 0, Spending 1, Hosting 0. The Overview one is Donate's key-limit note, which moves when step 2 moves Donate. The Spending one is an empty-state line in Spend by goal, which step 4 moves out of the centre. These are mock numbers; the live re-measure against the before table in [dc_8n3on7i7l6](../../note/2026-11/2026-11-03-bank-sheet-build-plan-gr-567tikzitl-file-level-inv-3on7i7l6.md) comes after deploy.
- **Plan for when it resumes:** if CI is green, merge #294 and redeploy, then park on the merge sha. Verify signed out on muster.town at 1400×900 and 390×844 using ~/shots/measure.mjs, upload a cropped picture of Overview, and rewrite topic pages [dc_we5nqevv40](../../wiki/2026-11/2026-11-03-bank-sheet-rebuild-gr-567tikzitl-plan-and-state-5nqevv40.md) and [dc_nb3743g7f6](../../wiki/2026-10/2026-10-29-the-bank-page-bankpanel-bankfinance-its-tests-and-3743g7f6.md).

## What I need from you
Nothing needed.
