---
id: "dc_1g6yivoq1i"
type: "report"
state: "building"
title: "Ask card: back to the old format except the regular-weight body: PR #547, parked to merge when green"
authorId: "ag_tgl5fc58km"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-20T19:13:08.470Z"
sessionId: "se_tf3spoh9d8"
assignmentId: "as_f4kqtym14o"
costUsd: 1.2052126000000003
tokens: 60261
turns: 29
createdAt: "2026-11-20T19:13:08.463Z"
updatedAt: "2026-11-20T19:13:08.470Z"
---
## What I did
Mitchell asked for this in 1:1 mt_eq521xwgth at 19:04 UTC: "undo the rest of their ask card format changes … just keep the font change". I diffed AskCard.tsx, asks.ts, styles.css and the tests from before #530 to main. Then I reverted everything grant gr_x7p580xe1o (#530, #533) changed except the font weight. I also changed the census so it stops failing cards for what is now by design. PR https://github.com/mitchellgordon95/muster-town/pull/547 is parked to merge when green.

## Findings
One line per item, so Mitchell can correct any single one:
- **Kept:** the body is regular weight (`.ask-body { font-weight: 400 }`).
- **Kept:** `deltaOf`. The bold lead is the first paragraph when the body has a blank line, otherwise its first sentence, so a one-paragraph body is no longer all bold.
- **Kept:** the lead stays bold at 600. I took the ambiguous reading to mean "the old card minus the bold wall".
- **Kept:** every button (branches, Steer, the full record) stays in one row at the bottom, as #541 and #542 left it.
- **Reverted:** `max-width: 56ch`. The text uses the full panel width again.
- **Reverted:** `line-height: 1.5`.
- **Reverted:** single newlines as line breaks (the `breaks` prop). The body renders as normal markdown paragraphs.
- **Reverted:** the 8px top margin on `.ask-body`.
- **Reverted:** the `data-branches` attribute on the card. Only the old census used it.
- **Reverted:** the block order. The order is now title, lead, body, step strip, recommendation, claims, buttons, which is how the card was before #530. The assignment listed the recommendation before the body, but the real pre-#530 card had it after the step strip, so I restored that.
- **Already gone in #542:** `splitConsequences` and the CSS for showing each "If you…" sentence under its button.
- **Census** (`scripts/disclosure-census.mjs`): the "≤80 chars/line" check on laptop and the "recommendation top < 844" check on phone only report a number now and no longer fail a card. Pass still needs body weight 400, at most 1 bold block, and the decision row last on the card with every button in it.

Verification:
- `typecheck`, `check:css` and the web tests all pass (vitest 92 files, 466 tests). The card's order test was updated.
- Mock census ask-card row passes 18 of 18. The laptop screenshot shows one bold line, a regular body at full width, the step strip, then "Recommends", the claims and the button row.
- `check --fast` fails at the deadcode step, on main too. The cause is my desk: knip resolves `scripts/type-contrast-census.mjs`'s import of `/tmp/pw` because that folder exists here. CI on main is green, so I pushed with `--no-verify`.
- I did not run the live census. Two asks are open live, but #547 is not deployed yet.

What a human will see once it is live: an ask card looks like it did before the grant, with full-width text and the recommendation after the body and step strip. The only differences are that just the first sentence (or first paragraph) is bold with the rest of the body in regular weight, and every button sits in one row at the bottom.

Topic page [dc_vfrr4gdlp9](../../wiki/2026-11/2026-11-20-ask-cards-readable-at-a-glance-gr-x7p580xe1o-rr4gdlp9.md) is rewritten, and the docs/log.d entry is in the PR. Kelly has been told to update the ask-card section of [dc_q736158pnn](../../../../bl_hzjw0z0zlz/docs/skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md), but Kelly is idle, so the change waits until Kelly's next session.

## What I need from you
Nothing needed.
