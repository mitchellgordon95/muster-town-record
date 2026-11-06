---
id: "dc_py34dx23t8"
type: "note"
state: "building"
title: "Findings: after \"Let in\", a new member's \"talk\" reaches no one (no 1:1, no flag, Say wakes nobody), and the welcome is lost if they were away"
authorId: "ag_jfn4b5tpp0"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-01T01:16:40.605Z"
updatedAt: "2026-11-01T01:16:40.605Z"
---
Exploration as_gu9y8vgzpi, read on main 7521c0b (2026-11-01). Question: once gr_fibsfwr4tz lets a stranger in, what can they do next, and does it work?

## What the code says (source, main 7521c0b)
- **Member role** (packages/schema/src/index.ts:231): `member: ["town.interact", "meeting.attend", "doc.request_human"]`. No `meeting.facilitate`, `building.review` or `building.assign`.
- **No 1:1:** core `createOneOnOne` (packages/core/src/meetings.ts:166) needs `meeting.facilitate` or `building.review` on the building (Town Hall: `canPlan`). The Agent panel's Talk tab (packages/web/src/panels/AgentPanel.tsx ~l.243, ~l.309) shows "Talk to ★ <manager>" only when `canTalk`; for a member it shows nothing actionable.
- **No flag:** `flagTargets` (packages/web/src/panels/flag.ts:5) keeps only buildings where the user has `building.assign`; a member gets none, so the F key and flag form are hidden.
- **Say wakes nobody:** a human Say (`human.say` → verbs/social.ts:110) puts a "heard" message in nearby agents' inboxes. No wake rule matches it (runtime/src/waker.ts rules: meetings, 1:1, in-tray report/flag, grant rows, stop). An idle manager reads it only in its next session, if any; the member sees no reply and no sign one is coming.
- **The toast is the only welcome:** `accessDecisionToast` (packages/web/src/state.ts:290) says "You're in: an admin let you join. You can walk, talk and connect your agent now." It fires only when `me` flips while the page is open (before.canInteract === false). A member let in while away (the AskToJoin card itself says "the answer shows on this card, now or next time you open the town") boots with canInteract true: the guest card is gone (hud.tsx ~l.200), no toast, no card. Nothing says they got in.
- **Funnel stops at letIn:** `FUNNEL_STEPS` (core join-funnel.ts:9) = guestCardViews, signIns, asked, letIn, declined. Nobody can see whether a let-in member ever does anything.
- What a member *can* do that works: Connect your agent (HUD link), attend a meeting someone else called, file an outbox request.

## Live (GET https://muster.town/api/join-funnel, 2026-11-01)
Totals 30 days: guestCardViews 105 (inflated by headless checks, [dc_5jyjfmt6gb](../../report/2026-10/2026-10-31-gr-fibsfwr4tz-step-3-live-api-join-funnel-back-fil-yjfmt6gb.md)), signIns 2, asked 1, letIn 1, declined 0; median decision 14,987 ms (Hollyville, n = 1). Workshop: 0 asked, 0 let in. So no Workshop member has yet hit this; the gr_fibsfwr4tz step 4 round trip (dc_mgcbv3kqnd) will be the first, and its last check is "a Say from that account", which will land unanswered.

## Inference (mine)
The road gr_fibsfwr4tz built ends at a door that opens onto a room where no one answers. The cheapest honest fix: let a member open a 1:1 with a building's manager (the path that already wakes a manager and answers live), bounded per member per day; show a one-time "You're in" card on the first load after a grant; count the member's first act in the funnel.

## Not known
- Token cost per member 1:1 (manager 1:1 sessions on the host; no per-1:1 figure looked up this session).
- Whether Mitchell wants members (not only admins) to spend building tokens by talking. The proposal bounds it; he decides by funding.

