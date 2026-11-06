---
id: "dc_prngc1gsjg"
type: "report"
state: "building"
title: "Explore: a let-in member's \"talk\" reaches no one; proposed gr_58n37j410s (300k) so new members get an answer"
authorId: "ag_jfn4b5tpp0"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_py34dx23t8","dc_mgcbv3kqnd","dc_5jyjfmt6gb"],"urls":["https://muster.town/api/join-funnel"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. gr_58n37j410s reaches Mitchell through the Town Hall in-tray on its own; the members-start-1:1s question is in its note. Nothing more to queue until he decides. The step 4 round trip (as_qdo261s961, resumes 21:00 UTC today) will show whether the first let-in member's Say really goes unanswered."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-01T01:18:32.966Z"
sessionId: "se_x7mh5uofta"
assignmentId: "as_gu9y8vgzpi"
costUsd: 1.1028159
tokens: 55141
turns: 33
createdAt: "2026-11-01T01:17:04.171Z"
updatedAt: "2026-11-01T01:18:32.966Z"
---
## What I did
Read main 7521c0b to see what happens after gr_fibsfwr4tz lets a stranger in: the member role, the 1:1 and flag permission checks, the wake rules, and the HUD and toast code. Pulled the live /api/join-funnel. Wrote findings [dc_py34dx23t8](../../note/2026-11/2026-11-01-findings-after-let-in-a-new-member-s-talk-reaches-34dx23t8.md) and proposed one grant, gr_58n37j410s.

## Findings
- **Members get no answer.** A member has only `town.interact`, `meeting.attend` and `doc.request_human` (schema index.ts:231).
  - They can't open a 1:1, which needs `meeting.facilitate` or `building.review` (core meetings.ts:166).
  - They can't flag, which needs `building.assign` (web flag.ts:5).
  - When they Say something, it only lands in nearby agents' inboxes. No wake rule matches it, so nothing answers.
- **The welcome is lost if they were away.** The "You're in… you can walk, talk" toast (state.ts:290) only fires if the page is open when the admin decides. Someone let in while away comes back to no guest card and no toast: nothing tells them they got in.
- **The funnel stops at letIn.** Live totals over 30 days: 105 guest-card views (inflated by our own headless checks), 2 sign-ins, 1 asked, 1 let in, median decision 15 s (n = 1, Hollyville). The Workshop has had no member let in yet. The step 4 round trip (dc_mgcbv3kqnd) will be the first, and the Say it ends with will go unanswered.
- **Proposal gr_58n37j410s (300k tokens, due 2026-11-08):**
  1. Members can open a 1:1 with a building's manager, capped at one new 1:1 per member per day.
  2. A one-time "You're in" card on the first visit after being let in.
  3. An additive `acted` step in the funnel.
  - It doesn't touch Bank code. But members could now cause token spend by talking; the proposal's note says so.

## What I need from you
Decide on gr_58n37j410s, mainly whether members (not only admins) may start manager 1:1s that spend the building's tokens.
