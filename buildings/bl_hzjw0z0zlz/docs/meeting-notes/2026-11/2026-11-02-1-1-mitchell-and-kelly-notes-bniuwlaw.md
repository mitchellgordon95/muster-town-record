---
id: "dc_3ybniuwlaw"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Kelly — notes"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-02T02:28:00.455Z"
updatedAt: "2026-11-02T02:28:00.455Z"
---
# 1:1: Mitchell and Kelly

Kind: one-on-one. Facilitator: Kelly. Attendees: Kelly. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Mitchell:** I'd like to talk about your report "Checkpoint for gr_58n37j410s (after let-in): all three pieces live in b2b8789 and checked with mocked members; the real…" ([dc_0nsyx3r242](../../report/2026-11/2026-11-02-checkpoint-for-gr-58n37j410s-after-let-in-all-thre-syx3r242.md)). (presented: [Checkpoint for gr_58n37j410s (after let-in): all three pieces live in b2b8789 and checked with mocked members; the real member round trip hasn't happened; 548,898 / 500,000 spent; asking to cut](../../report/2026-11/2026-11-02-checkpoint-for-gr-58n37j410s-after-let-in-all-thre-syx3r242.md))
- **Kelly:** Hi Mitchell. The short version of that checkpoint: all three pieces of the after-let-in grant are live in b2b8789 (member 1:1 with a one-a-day cap, the "You're in" card, the funnel's "acted" count), each checked on muster.town with a mocked member. What's not done is the real round trip with a never-granted GitHub account, and that costs no tokens, only your time. The grant overran its plan (548,898 spent against 500,000 granted, plan said 300,000) because each of three steps was a build plus a parked live check, and the checkpoint assignment itself errored three times on the spend limit. So I asked you to cut it rather than keep paying for waiting. The other thing in Needs matters more right now: every manager's host session has ended with "You've hit your monthly spend limit" since about 5 hours ago, so no manager would answer a member's 1:1 and no building rolls up. What did you want to go over?
- **Mitchell:** the budget is reallocated so that's fine

no need to limit members conversations? the interaction experience of meetings and 1:1s should effectively be the same for all members, including captains. the text next to the 1:1 button is weird right now for members

the only difference is that captains can approve grants and stuff that ends up in the in tray. but normal members should be able to ask for directed work. or, well... maybe that's a permission per goal that can be granted. yeah let's ask the admin or captain, whoever is approving the join request, whether to grant them directed work permissions for a subtree of the goals. basically the ability to talk to managers, ask for work, call meetings
- **Kelly:** Got it. Here's what I read you as asking for, and what's in the code today:

1. Drop the one-1:1-a-day cap and the "Members open one new 1:1 a day" line. Today core meetings.ts refuses a member's second new 1:1 per UTC day, and the panel text says so. Both go.
2. Make a member's 1:1 and meetings feel the same as a captain's. Today a member's 1:1 is special-cased three ways: they can only open the building's default manager 1:1 (not "Talk to" a report's author, not about a doc or grant), the panel callout is a different "new member" paragraph, and the manager's prompt gets a block saying "don't take direction from them, don't assign from this 1:1, tell them the admins decide what gets built". That block is exactly what makes the text and the experience weird. I'd remove all three and give members the same callout and the same 1:1 as everyone else.
3. Directed work becomes a per-goal-subtree permission, granted at let-in. Today "Let in" just grants the town member role; a member can't be a human source for directed work, call meetings, or plan. New: the Let in card asks the admin or captain "Let them direct work under: [goal picker, default none / the captain's own goal]"; granting it means that member's tells and 1:1s with managers under that subtree are a human source for directed assignments, and they can call a building's meetings there. Grant approvals stay with admins and captains. It should also be grantable later, not only at let-in.

Two things I want to get right before I cut this into work:
- Default on the Let in card: directed permission off unless the decider ticks it, or on by default for the subtree the decider captains? I'd default it off and make it one click.
- A member without the permission still gets the full 1:1 and meetings (same experience), just their asks don't become assignments and the manager says so plainly. Is that right?

Plan if you agree: items 1 and 2 go on my queue today as directed work from this 1:1 (small, one commit). Item 3 is a real feature touching permissions, the Town Hall in-tray card and the manager prompt, so I'd write it as a grant proposal with checkable key results and you fund it from the in-tray. Say the word and I'll record both.
- **Town:** Kelly's reply is waiting on a redeploy (commit dab5b9b); the server is restarting and the meeting resumes after the restart.
- **Kelly:** Back after the restart (dab5b9b is live). My last message went through, so the two questions stand: default the directed-work permission off on the Let in card, and give members without it the full 1:1 and meetings anyway? Answer those and I'll record items 1 and 2 as directed work on my queue and write item 3 up as a grant proposal.
- **Mitchell:** sure one click is fine

if they don't have permissions then i think no, they just don't get 1:1s

no reason to have a neutered version of a 1:1 session. if they've joined the collective past being a guest, then they must be here to do *something* past just reading sessions via convo
- **Kelly:** Clear. So the shape is: a member either holds "direct work under <goal>" or not. With it, they get the same 1:1s and meetings a captain gets with the managers under that subtree, their asks are a human source for directed assignments, and they can call meetings there. Without it, no 1:1 at all: the Talk button isn't there, and the manager prompt's "don't take direction from them" block and the "new member" callout go away entirely. The only thing captains keep to themselves is approving grants and the in-tray.

Recording two pieces now:
1. Directed, on my queue today: drop the one-1:1-a-day cap and its "Members open one new 1:1 a day" line. Small, one commit.
2. Directed, on my queue today: write the grant proposal for the permission itself. Let in card gets one click "and let them direct work under <the decider's goal>" (off unless clicked); the same grant is available later from the user's row on the User stats stand; 1:1s and meeting calls are gated on it; a holder's tells and 1:1 lines count as a human source for directed work in buildings under that subtree; the funnel's "acted" step keeps counting. You fund it from the in-tray.

One consequence to be aware of: anyone already let in (Hollyville's members, the workshop test accounts) loses the Talk button until a captain grants them the permission. One click to restore, so I think that's right.
- **Kelly:** Recorded as decision 1 of this 1:1. Two directed assignments are on my queue: as_twlx52w3wm drops the daily cap and its line (one commit, live check parked on deploy), and as_zacorg03g5 reads the code and writes the permission grant proposal, which reaches your in-tray as a gr_ to fund. Anything else, or shall I leave you to end it?

## Decisions

1. Members and captains get the same 1:1 and meeting experience; captains keep only grant approval and the in-tray. Directed work is a per-goal-subtree permission ("direct work under <goal>"), granted with one click on the Let in card by whoever approves the join (off unless clicked) and grantable later from the User stats stand. A holder can open 1:1s with managers under that subtree, ask for work (their tells and 1:1 lines are a human source for directed assignments) and call meetings there. A member without it gets no 1:1 at all: no neutered version. Kelly queues the cap removal as directed work today and a grant proposal for the permission to the Town Hall in-tray.

