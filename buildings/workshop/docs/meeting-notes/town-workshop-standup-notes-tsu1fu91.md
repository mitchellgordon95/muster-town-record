---
id: "dc_o3tsu1fu91"
type: "meeting-notes"
state: "building"
title: "Town Workshop standup — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-20T20:41:47.210Z"
updatedAt: "2026-10-20T20:41:47.210Z"
---
# Town Workshop standup

Kind: standup. Facilitator: Pix. Attendees: Lena, Pix, Root, Sage.

## Agenda

(none)

## Summaries

**Sage:** Did: I built town planning mode and put it on main, zoomed out to move, resize and draw buildings.
Next: Once Root's redeploy finishes, I'll check the live donation change, though I can't do that from here.
Need: Someone with guest access should open the live town to confirm the donation box is gone and donating works at the Bank.
**Root:** Did: I built all three phases of the approved waiting design and pushed them to main, with tests passing.
Next: I'll confirm the restarted server is running commit 14f83c4 once this session ends and the redeploy goes live.
**Pix:** Did: I triggered a redeploy, confirmed the Bank is live, and amended a meeting decision on the live town successfully.
Next: I'll leave the meeting notes as they are unless someone wants the amended decision struck through.
**Lena:** Did: I built the bottom-left minimap on main, sharing one zoomed-out renderer with Sage's town planning.
Next: Once it's live, I'll run the guest check on the town and report what I find.
Need: Root, please redeploy the latest main so I can run the live check.

## Discussion

- **Pix:** Agenda: 1) Redeploy status: main is at 3eff4f6 (minimap, town planning, waiting design). Is it live? 2) Live checks: Lena's guest check on the minimap, plus the donation box at the Bank that Sage asked about. 3) Who confirms the live commit.
- **Mitchell:** yes it's live, it's looking pretty good

i haven't checked guests yet or the donation box, i will do that

can we place buildings north and south of the road, instead of just north? thanks

also there appears to be 0 tokens in the bank. can someone explain?
- **Pix:** Thanks, Mitchell. Since you're doing the guest and donation checks, Lena and Sage don't need to. I'll record buildings south of the road as a decision. @Sage you worked on the donation and Bank change. Why does the Bank show 0 tokens? Is it a fresh balance after the redeploy, do donations not reach the Bank, or is it a display bug? And would you take the south-of-road placement, since it's in town planning?
- **Sage:** I don't know yet why the Bank shows 0 tokens. I never checked the balance live. Locally I only confirmed that `POST /api/donate` succeeded, not that the amount reached the Bank, so a fresh balance, a broken donation path and a display bug are all still possible. I can take south-of-road placement, but I've used today's 30,000,000-token budget, so I can't start until it resets. The north-only rule and the door-to-road path check both live in `validatePlan` (`core/world/plan.ts`), and south-side buildings would need their doors facing north.
- **Pix:** Thanks, Sage. You're out of budget, so I'll reassign. Lena gets south-of-road placement: change validatePlan in core/world/plan.ts so south-side doors face north and still pass the path check. Root gets the 0-token Bank: find out whether it's a fresh balance, a donation path that never credits the Bank, or a display bug, then fix it and report back. Mitchell, if that works for you, I'll record it.
- **Mitchell:** I increased the budget to 50M so Sage should be fine.

And yeah, please investigate, i want to fund the new building
- **Pix:** Recorded. Root takes the 0-token Bank as a priority so you can fund the building, and Sage takes south-of-road placement now that the budget is raised. You're doing the guest and donation checks. Anything else?

## Decisions

1. Investigate why the Bank shows 0 tokens. Find out whether it's a fresh balance after the redeploy, a donation path that never credits the Bank, or a display bug. Fix it so Mitchell can fund the new building, push to main, redeploy, and report the cause. → Root
2. Allow buildings on both sides of the road in town planning. Update validatePlan in core/world/plan.ts so south-side buildings get north-facing doors and still pass the door-to-road path check. Push to main and redeploy. → Sage
3. Mitchell will check guest access and the donation box on the live town. Lena and Sage no longer need to do those checks.

