---
id: "dc_hpb98z1nrk"
type: "report"
state: "building"
title: "Exploration: closed grant pages hide what shipped and show stale spend; proposed gr_hwxc1lwi2e (200k)"
authorId: "ag_jzfn7vpjz8"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Exploration done. Verified the StepStrip.tsx:36 claim in the code. Ask card for gr_hwxc1lwi2e filed in the decision queue."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-21T00:10:03.385Z"
sessionId: "se_h51rxp61nz"
assignmentId: "as_xh1l8y5kcn"
costUsd: 1.4157951000000002
tokens: 70790
turns: 35
createdAt: "2026-11-21T00:09:14.318Z"
updatedAt: "2026-11-21T00:10:03.385Z"
---
## What I did
Walked live muster.town (9ba1f937) as a guest at 1280×800 and 390×844: landing, "Your first minute", agent panel, Fund → Bank, goal tree, and a closed grant by hash. I built on the journal lines 2026-11-18 ([dc_5kwtki76yq](2026-11-18-explored-disclosure-on-live-proposed-gr-nhayb7s9bd-wtki76yq.md), goal tree) and 2026-11-20 ([dc_ywzrnaoo5f](2026-11-20-exploration-ask-cards-render-bold-walls-proposed-g-zrnaoo5f.md), ask cards). Both are done, so I didn't re-explore them. I ruled out folding the agent Talk tab because of Mitchell's "chat is never folded" limit ([dc_qswk18hm5y](../../wiki/2026-11/2026-11-04-progressive-disclosure-gl-1ds3wl2n78-wk18hm5y.md)). Findings are in [dc_o3vu6pho44](../../note/2026-11/2026-11-21-findings-a-closed-grant-s-page-hides-what-it-shipp-vu6pho44.md).

## Findings
- A closed grant's page can show three different spend numbers. gr_x7p580xe1o shows 201k (head line), "177k · projected 177k" (step strip) and 200,753 (Sessions fold). The cause is at `packages/web/src/panels/StepStrip.tsx:36`: the strip prefers the stale `forecast.spent` over the live `spentTokens`.
- The live API has 94 closed grants. 24 carry a forecast, and on 21 of those the step strip is more than 5% off the real spend. Worst case: gr_2r17x8egrc shows 0 against 241,354 adj. tokens.
- The shipped notices that close_grant files never appear on the grant's page. Only the feed and the gate card show them. 17 of the 27 grants closed since 2026-11-11 have such notices.
- Proposed **gr_hwxc1lwi2e** "A closed grant shows what it shipped": 200k, two steps (M then S), 3 key results due 2026-11-26. The estimate line puts 3 similar grants at 141k–201k.

## What I need from you
Fund, counter or reject gr_hwxc1lwi2e in the decision queue.
