---
id: "dc_j1xwifpsus"
type: "report"
state: "building"
title: "Grant B step 2: PR #380 open (grant card + deck slide list the steps with their state); parked on CI"
authorId: "ag_1cll401202"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #380 (grant card + deck slide list the steps with state) parked on CI; its continuation as_k9pld06wff merges if green, parks on the deploy, then takes the live screenshot. Step 3's wait on as_7dbotftl4e follows the park chain (core waits.ts chainTip), so it holds until the screenshot lands. No action needed."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T22:48:21.172Z"
sessionId: "se_w2j3z0tz41"
assignmentId: "as_7dbotftl4e"
costUsd: 1.4600847
tokens: 73004
turns: 36
createdAt: "2026-11-05T22:47:59.276Z"
updatedAt: "2026-11-05T22:48:21.172Z"
---
## What I did
Built grant B step 2 (gr_b5fyqibfx2, kr_snardl39qh) and opened draft PR https://github.com/mitchellgordon95/muster-town/pull/380. Then parked on its CI.

## Findings
- **Grant card:** `GrantSteps` in web panels/Places.tsx sits inside the GrantRow plan list, so it shows on the grant page and on the in-tray row. It lists the steps numbered. Once a grant is funded, each step also says queued, running, done or cancelled. That state comes from the new `GrantView.stepStates`, which core grants.ts builds from the latest assignment for each `grantStep`. A parked step's continuation keeps its step number, so the latest assignment is the right one to read.
- **Deck:** the proposal slide in review-deck.ts has a "**Steps** (funding queues step 1; each step's report queues the next)" block under "What it is", built with the schema helper `grantStepLines`.
- **Docs:** I added a sentence to docs/goal-directed-budgets.md. docs/wakes.md and the funding/next-step wording already came in with step 1 (#377), so I didn't change them.
- **Tests:** new tests in core test/grant-steps.test.ts (the deck slide text, and states going done → queued → none) and in web test/grantSteps.test.tsx. Typecheck passes. Locally core 805/805, server 297/297 and web 363/363 pass. The web run also shows one "happy-dom not found" error that happens the same way on main at this desk, so it isn't from this change.
- **Not done yet:** the screenshot of the live card. The task asks for one from the live town, so it has to wait for the deploy. The continuation merges if CI is green, parks on the deploy, and then takes a screenshot of a proposal card such as gr_8bxoy2heif.

## What I need from you
Nothing needed.
