---
id: "dc_oqhp31yd2d"
type: "report"
state: "building"
title: "Ask card: every button together at the bottom: PR #541, parked to merge when green"
authorId: "ag_v009tvdbf3"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-20T18:20:38.463Z"
sessionId: "se_onki4otb2l"
assignmentId: "as_4wqws17n8y"
costUsd: 1.4753207999999995
tokens: 73766
turns: 28
createdAt: "2026-11-20T18:20:38.454Z"
updatedAt: "2026-11-20T18:20:38.463Z"
---
## What I did
Mitchell said in the 1:1 with the Secretary: "putting buttons in the middle of the text is weird, put them all back together at the bottom." I moved every button on the ask card into one row at the bottom, below all the text. PR https://github.com/mitchellgordon95/muster-town/pull/541 is parked to merge when its checks pass.

## Findings
- The card's new order (AskCard.tsx): title, bold lead, recommendation, body, the "If you <branch>:" sentences as one list, step strip, claims. Then one row holds the branch buttons and Steer, followed by "The full record →". Before this, each button sat in the middle of the text with its own sentence under it, and Steer was in a separate footer row.
- Signed out, or signed in without the right to decide: the text comes in the same order. The bottom row holds Steer (if any) and "Sign in to decide." or "A captain or admin decides this."
- If an ask has no buttons it can wire, Steer still shows in the row.
- I changed the disclosure census: on a phone it now prints the button row's top but no longer fails a card because of it. With the buttons at the bottom by design, a long card has to scroll to reach them. The phone check that still counts is the recommendation's top being under 844 px.
- Checks: typecheck is clean and all 472 web tests pass (the ask-card order tests were rewritten). Mock census of the ask cards: 18 of 18 pass at 1366×800 and 390×844. The laptop screenshot shows the text, then the step strip and claims, then one row with Adjust…, Cut and Steer.
- I updated the topic page [dc_vfrr4gdlp9](../../wiki/2026-11/2026-11-20-ask-cards-readable-at-a-glance-gr-x7p580xe1o-rr4gdlp9.md) with the new layout.

## What I need from you
Nothing needed.
