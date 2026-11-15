---
id: "dc_oa8mlpmc5q"
type: "report"
state: "building"
title: "Ask card leads with \"<Building> is asking for …\": PR #451, parked on CI"
authorId: "ag_0sa9bqw448"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. PR #451 (ask card opens with \"<Building> is asking for money/a credential/…\" at fs-xl) is parked on CI; as_w8tg893vob squash-merges it when green. Nothing else queued."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-15T19:07:32.847Z"
sessionId: "se_chem3chje0"
assignmentId: "as_5q831zixel"
costUsd: 1.3360536
tokens: 66803
turns: 32
createdAt: "2026-11-15T19:07:16.673Z"
updatedAt: "2026-11-15T19:07:32.847Z"
---
## What I did
I replaced the small grey type pill at the top of the ask card with one big sentence. Then I checked it in the mock town at 1280×800 and 390×844 and opened PR #451: https://github.com/mitchellgordon95/muster-town/pull/451

## Findings
- `packages/web/src/panels/AskCard.tsx`: the card now opens with "Workshop is asking for **money**", in --fs-xl (22 px). It also reads "for a **credential**", "a **meeting**", "a **policy** decision", "a **click**", and for a do ask "is asking you to **do something**". The bold word for money is in the warn colour. The Town Hall reads "The Town Hall", and asks with no building read "The town". The rank pill and the age stay small beside the sentence. The title stays below it at --fs-lg.
- Decision queue, one at a time: it reads well on desktop and on phone. On a phone the sentence wraps to two lines and the rank and age drop beneath it.
- Funding view: the sentence heads each card and looks fine.
- List view: unchanged. It keeps its own small kind pill per row, which suits a list.
- Review deck: unchanged. It only uses the card's buttons.
- Tests: askCard.test checks the sentence. All 423 web tests pass, and `check --fast` is green.
- Desk note: if playwright-core is installed at /tmp/pw, knip flags `scripts/type-contrast-census.mjs` because of its absolute import. Delete /tmp/pw before running `check`.

## What I need from you
Nothing needed. This is parked on PR #451's CI, and I squash-merge it when it is green.
