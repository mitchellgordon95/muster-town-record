---
id: "dc_r5ta9ejnkq"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-02T03:27:43.194Z"
updatedAt: "2026-11-02T03:28:13.257Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Mitchell:** I'd like to talk about the proposal "A captain steers within a budget the captain above them sets: a stranger who becomes a captain can fund grants and set …" (gr_kph1zjjrzg), for key result kr_irf94gdti3: "A captain above (or an admin) sets a monthly token budget on a captained goal, and its detail shows how much is used". (presented: Grant: A captain steers within a budget the captain above them sets: a stranger who becomes a captain can fund grants and set exploration only up to that ceiling, and sees what's left of it. (page grant:gr_kph1zjjrzg))
- **Pix:** Here's what that key result would build. Today a captain can fund any grant in their subtree with no ceiling (Grants.canFund, and since your change funding is never refused, the shortfall just goes overdrawn). So a stranger you accept as captain gets unlimited draw on the Bank. The KR adds one number per captained goal, budgetTokensPerMonth, set only by the captain above or an admin. The goal's detail shows "Budget: X of Y used this month", where X is the grants funded under that node this month. A captain can't fund past it; you and captains higher up stay ungated as today. Two choices I'd like from you: (1) the default for a newly accepted captain: 0 (they can decide and counter, funding waits for a budget) or uncapped; Pix 2 proposed 0. (2) The period: UTC calendar month, or rolling 30 days. What did you want to change or ask?
- **Mitchell:** probably the framing. idk if we have a vision doc lying around somewhere, or if explorers are instructed to read it, but we have some opinions on how the economy works here

basically i think it's fine that the bank is the source for all grants. if the work gets approved, then it should get done

what we might limit for subtrees (specifically subtrees with other captains) would probably be desks total assigned to the subtree (which would limit concurrency and therefore burn rate) and / or exploration cap (which would keep them from burning through the whole budget on exploration, but they'd inherit the root's cap anyway, so i don't think you need to set this)
- **Pix:** Got it: approved work gets done from the Bank, no per-captain token budget. Three things from that. (1) The vision doc exists, docs/how-work-gets-done.md on main, but the explore tick's assignment text (core explore.ts startExplorer) never points at it, so Pix 2 proposed against the economy without reading it. I'll fix that: the explorer's brief names the doc and its §7-8 (Bank pools, free tokens, caps) as required reading. (2) One correction on "they'd inherit the root's cap anyway": true until they set their own. Goals.update lets a captain set exploreCapTokensPerDay on their own goal and exploreCapAt takes the nearest cap, not the tightest, so a captain below can loosen the root's 500,000. Making it the minimum on the path is a small change; I'd keep that. (3) Desks per subtree as the real throttle: a captain above sets a desk total on a captained goal; the desk count across the subtree's buildings can't exceed it, and the goal's detail shows "N of M desks". That caps concurrency and burn rate. If you counter gr_kph1zjjrzg in the in-tray, I'll rewrite it as those three: explorer brief, min-cap rule, desk total per subtree. Or reject it and I file fresh. Which do you want, and is a desk total the right unit or should it be something else?
- **Mitchell:** while you're at it, you should be able to withdraw and then repropose a grant, right?
- **Pix:** Half right. The API has it: POST /api/grants/:id/close with outcome "stopped" lets a manager withdraw a proposed grant (core grants.ts close, line 475). But the manager's town tools don't expose it: close_grant only closes a funded grant as done and refuses a proposed one, and re-proposing under the same id only works after a counter. So today I can't withdraw gr_kph1zjjrzg myself; you'd have to reject it. I'll queue the fix as directed work from this 1:1: a withdraw_grant tool (manager, proposed grants only, with a note that shows in your in-tray as the reason), then I withdraw gr_kph1zjjrzg and file the rewritten one (explorer brief reads the vision doc, min-cap rule, desk total per subtree). That drops my counter-or-reject question. Still want your answer on the unit: desk total per subtree, or something else?
- **Pix:** Queued: as_r8wz26kata builds withdraw_grant (manager, proposed grants only, a note that stays on the grant so you see why it left the in-tray), then withdraws gr_kph1zjjrzg once live. The rewritten proposal waits on your answer about the unit.
- **Mitchell:** desk total per subtree, yes

also let's carefully consider what happens to the economy and book keeping when an approved, in-progress grant is withdrawn (if we let that happen at all)
- **Pix:** Desk total per subtree: noted, it goes in the rewrite. On withdrawing a funded grant, I read the code and the gap is real: the API already lets a manager close a funded, in-progress grant as "stopped" (grants.ts close, l.480-486), with no bookkeeping around it. What happens today: (1) Spent stays correct: a grant's spend is a SUM over its sessions by grantId, never stored, so past sessions keep their booking. (2) The unspent rest returns to free tokens the moment it closes, because earmarks and the overdraft walk count only funded/checkpoint grants. That's the risk: a fork still running on it keeps spending, its session still books to the grant, but the money it draws is now promised to the next overdrawn grant in the walk. (3) Queued grant-lane assignments go to "held: grant closed" and sit forever; nothing cancels them or stops running forks. (4) Key results stay open; only closeDone claims them. (5) A member-funded grant (fundWith) returns its rest to the general pool, not to that member's input. My proposal: withdraw_grant stays proposed/countered only, no money has moved, so nothing to book (that's what as_r8wz26kata builds). For funded grants, stopping stays a human-only act (the web Close grant button needs building.fund) and gets a defined sequence: stop its running forks first and wait for their reports, cancel its queued grant-lane assignments, then close; spend stays as booked, the rest goes back to whoever funded it, open key results are archived as missed with the note, and the close shows in your in-tray with the reason. Want that sequence in the rewritten proposal as a fourth key result, or as its own grant?
- **Mitchell:** probably its own grant
- **Pix:** Recorded as two decisions, both mine, both waiting on the withdraw tool (as_r8wz26kata): (1) withdraw gr_kph1zjjrzg and re-file it with three key results: explorer brief reads the vision doc, exploration cap is the minimum on the path, desk total per captained subtree shown on the goal's detail (as_9y6fgxo276). (2) Stopping a funded grant as its own proposal with the sequence I described: human-only, stop forks and wait for reports, cancel queued assignments, close, rest back to whoever funded it, open key results missed with the note, reason in your in-tray (as_3zgq6c3wqw). Both proposals land in your in-tray to fund, counter or reject. Anything else on this one?
- **Mitchell:** i went ahead and rejected gr_kph1zjjrzg
- **Pix:** Good, that saves a step. Pix 1 is mid-build on the withdraw tool; I told it to drop the "withdraw gr_kph1zjjrzg" half and ship the tool alone. The two proposals no longer need to wait on it, so I'm re-queueing them to start now: the fresh captain-subtree proposal (explorer brief, min cap, desk total) and the funded-grant stop proposal. Both reach your in-tray on their own.

## Decisions

1. No per-captain token budget: the Bank funds every approved grant. gr_kph1zjjrzg is withdrawn (once the withdraw_grant tool is live, as_r8wz26kata) and re-filed as a fresh proposal with three key results: the explore tick's brief names docs/how-work-gets-done.md as required reading; exploration caps combine as the minimum on the path; a captain above (or an admin) sets a desk total on a captained goal that the subtree's buildings can't exceed, shown on the goal's detail. → Pix
2. Stopping a funded, in-progress grant is its own grant proposal: human-only (building.fund), stop its running forks and wait for their reports, cancel its queued grant-lane assignments, then close; spend stays as booked, the unspent rest goes back to whoever funded it (a member's input, else the pool), open key results archive as missed with the note, the reason shows in the Town Hall in-tray. Filed as a proposal for Mitchell to fund, counter or reject. → Pix

## Decisions recorded after close
- (replaces decision 1) Mitchell rejected gr_kph1zjjrzg himself (03:27Z), so decision 1 no longer waits on the withdraw tool: the fresh captain-subtree proposal (explorer brief reads docs/how-work-gets-done.md, exploration cap = minimum on the path, desk total per captained subtree on the goal's detail) is queued now as as_u9e1x19y3o. The withdraw_grant tool (as_r8wz26kata, Pix 1) ships alone, without withdrawing anything.
- (replaces decision 2) Decision 2 likewise starts now: the "stop a funded grant" proposal (human-only; forks stopped and their reports in, queued grant-lane work cancelled, then close; spend stays booked, the rest back to whoever funded it, open key results missed with the note, reason in the Town Hall in-tray) is queued as as_8a5bywnqw0.

