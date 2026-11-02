---
id: "dc_jela5ondmt"
type: "report"
state: "building"
title: "gr_vipnoft4gk closed as done: the manual's word cap now fails `check:docs` in under a second with count, overage and largest sections (PR #177 → 34b7e53, CI green attempt 1); kr_cm5qb2wqh7 claimed"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_ic2819wkgu"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/177","https://github.com/mitchellgordon95/muster-town/actions/runs/41237691015"]}
tags: ["rollup","grant-close"]
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-31T20:35:24.675Z"
sessionId: "se_zd2kx8ktc0"
assignmentId: "as_lldzy7s8ww"
costUsd: 3.6754212499999994
tokens: 73508
turns: 27
createdAt: "2026-10-31T20:16:45.616Z"
updatedAt: "2026-10-31T20:35:24.675Z"
---
Live should be 8a3a510 (main after my merge 34b7e53 plus Pix's #178; redeploy called 20:10Z, not waited for).

## Shipped

**1. The manual's 1900-word cap is checked first, fast and explicit, instead of 60–90 s into the tests**
**What it is:** The cap moved out of a web unit test into the docs check, the first step of `npm run check` and CI (PR #177, merge 34b7e53). Over the cap it fails in under a second with the word count, the overage and the five largest sections; under the cap with fewer than 50 words left it prints a warning, so authors trim in the same PR instead of a follow-up commit (10 such trim commits since 10-28). One sentence in AGENTS.md names the cap and where it is checked. The cap number and the manual's content are unchanged. No pre-push hook. I did it myself in the funding session (one PR; a fork would have cost more to brief than to build). Findings behind the plan: [dc_s36jzsjfd0](../../note/2026-10/2026-10-31-recurring-red-ci-the-manual-s-1900-word-cap-and-di-6jzsjfd0.md).
**What you'd see:** Command-line only, no picture. On main, `npm run check:docs` ends with `docs/manual.md: 1894/1900 words, only 6 left under the cap: trim before adding to it` and passes (0.6–1.2 s on a desk; the same line is in the CI log of main run 41237691015). On a branch with 60 words appended: `docs/manual.md: 1954 words, 54 over the 1900-word cap. Largest sections: Steering 312, Talking to agents 269, Running a collective (admins) 246, Funding 222, Start your own collective 196. Trim it in this change.` and exit 1 in 0.56 s. PR run 41237347607 and main run 41237691015 green on attempt 1. (Main run 41237582164 for 34b7e53 itself shows "cancelled": Pix merged #178 a minute later and the workflow's cancel-in-progress rule stopped it after its check steps had already passed; not a failure.)
**Your call:** None. The manual has 6 words of headroom, so the next edit to it will have to trim something; that is now visible at the top of every check instead of at the end.

## Decided
- [dc_ic2819wkgu](2026-10-31-ci-exploration-kr-cm5qb2wqh7-no-flakes-the-manual-2819wkgu.md) → approved earlier today (the exploration that found the cap as the top CI toil; the grant's plan came from it).
- The separate wake for the rejected 60k proposal gr_9nvxjgajh6 (as_xwyhh56vms) will be closed with "nothing follows": the rejection was what the 30k proposal's note asked for.

## Key results
| Key result | Status | Spent / granted |
|---|---|---|
| kr_cm5qb2wqh7 CI on main stays green without reruns (gr_vipnoft4gk, closed as done) | claimed | 48,068 / 500,000 (the funding assignment said 30,000; the grant record says 500,000; 451,932 returned to the Bank) |

Evidence for "claimed": no flake in the last 200 main runs ([dc_ic2819wkgu](2026-10-31-ci-exploration-kr-cm5qb2wqh7-no-flakes-the-manual-2819wkgu.md)); the two known flakes fixed at the root earlier (PR #72, PR #85); the top recurring red cause (manual cap, twice on 10-30) now fails at the docs step before a push can reach the tests; last 30 main runs green on attempt 1. The one red cause left is a direct push to main that skips PR CI, which only branch protection (your setting) prevents.

Today's spend by lane: exploration 48,539 tokens (free under the goal: 5,304,155), directed 0 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 0 proposals, 1 request ([dc_bn4s4m7cq3](../../../../../town-hall/outbox/2026-10/2026-10-29-redeploy-with-the-desk-image-rebuild-image-true-fo-4s4m7cq3.md)), 0 rollups._
