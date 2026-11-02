---
id: "dc_0kycc1y69h"
type: "report"
state: "building"
title: "Talk to <name> now on every agent-authored doc and on grants (1501b4a pushed, redeploy queued); live check parked"
authorId: "ag_64el7tvtt9"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "1501b4a shipped; its live check already ran as as_ye4l0b8hdq (Pix 1, dc_6u5s83cpv): button on articles and grant cards verified, screenshot mf_2k6vom1azj, wording fix 5502ae1 on main. Nothing further."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T04:30:54.811Z"
sessionId: "se_b0jkx8k4ia"
assignmentId: "as_qzq4u7hllw"
costUsd: 1.7740510000000005
tokens: 88703
turns: 43
createdAt: "2026-10-29T04:17:40.830Z"
updatedAt: "2026-10-29T04:30:54.811Z"
---
## What I did
Built Mitchell's ask from 1:1 mt_u6euky43hg and committed it straight to main as **1501b4a**. Queued a redeploy. Nothing is live-checked yet: this report parks on {deploy: 1501b4a}.

## Findings
- **Docs.** DocView now shows **Talk to <name>** on every doc type whose author is an agent (article, note, source, meeting-notes, deck, wiki, skill, fyi, notebook, assignment-proposal, report). Who sees it is unchanged: a signed-in human with meeting.facilitate or building.review. Docs written by humans have no button: core `oneOnOneTarget` and web `talkTarget` now return null when the author's kind is human. The fork → manager wording is kept. The button's tooltip names the doc type, e.g. "about this article".
- **Grants.** `GrantRow` (packages/web/src/panels/Places.tsx) now shows **Talk to <name>** next to the grant id. `GrantRow` is used by both the Town Hall in-tray and the grant panel `/#/grant/<id>`, so the button appears on every status there. The target is the proposer, resolved the same way as a doc's author, as long as it works in the grant's building; otherwise it's the building's manager (web `grantTalkTarget`, core `createOneOnOne`).
- **Route.** POST /api/buildings/:id/one-on-one now takes `{agentId?, docId?, grantId?}`; the report path is unchanged. With `grantId`, the human's first line reads: *I'd like to talk about the proposed proposal "<objective>" (gr_…), for key result kr_…: "<text>".* It is attached as page `grant:<id>`. The grant is presented once per meeting. A grant from another building gets 400 and an unknown grant gets 404. The 1:1 prompt tells the agent that the grant id and its key result are in that first line.
- **Tests.** Typecheck is green. Suites: core 434/434 (adds a test for an article, a human author and a grant), web 114/114 (talkToAuthor.test.tsx covers an article, a human note with no button and a GrantRow), server rest.test.ts 21/21 (new grantId case), runtime one-on-one 4/4. `check:deadcode` did **not** run: `knip` isn't installed on this desk (exit 127).
- Topic page [dc_vrrph0d7ss](../../wiki/2026-10/2026-10-28-talk-to-the-author-1-1-docs-and-grants-rph0d7ss.md) is renamed to "Talk to the author (1:1): docs and grants" and rewritten. The next session updates [dc_oghes5lgud](../../wiki/2026-10/2026-10-28-grants-key-results-and-the-town-hall-in-tray-hes5lgud.md) and makes the screenshot after the live check, so there is **no screenshot id yet**.

## What I need from you
Nothing needed.
