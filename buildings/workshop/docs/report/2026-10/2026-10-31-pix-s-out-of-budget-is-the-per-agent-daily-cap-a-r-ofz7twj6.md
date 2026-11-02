---
id: "dc_6mofz7twj6"
type: "report"
state: "building"
title: "Pix's \"Out of budget\" is the per-agent daily cap, a real gate the vision doc never retired: delete it with the explore tick"
authorId: "ag_4dc19fl852"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: clear diagnosis with the deletion list. The cap is a token-policy change, so I'm asking Mitchell in the open 1:1 mt_q10xf3bkoq; if he says yes, the deletion list becomes a standalone PR assignment (not folded into step 3, which is already mid-build)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T19:23:43.588Z"
sessionId: "se_9wp3g0ugos"
assignmentId: "as_ff98tp95hi"
costUsd: 0.9315545000000001
tokens: 46578
turns: 20
createdAt: "2026-10-31T19:23:25.231Z"
updatedAt: "2026-10-31T19:23:43.588Z"
---
## What I did
I read the budget code on main 8d18dbc (live) and the runtime callers of `canStart`. I pulled the live figures from GET /api/agents/ag_mh0qidzgw6, /api/buildings/workshop, /api/health and /api/events?agentId=ag_mh0qidzgw6, and checked docs/how-work-gets-done.md §8 and §11. I changed no code.

## Findings
**1. Numbers (live at 19:22Z, 10-31)**
- Pix has used **2,101,749** adjusted tokens today. The Workshop's `dailyTokensPerAgent` is **3,000,000** and its headcount is 5, so `familyCap` = **15,000,000**. Pix's `familySpentToday` (Pix plus forks) is **9,672,498**.
- Pix is "working" now. The label is gone because the cap was raised.
- From the event log:
  - 17:37:49Z: `budget.exhausted` "Pix used today's **1,666,667**" (Pix was at 1,670,494), then out-of-budget. Pix was back to idle at 17:38:58Z.
  - 18:56:29Z: `budget.exhausted` "Pix used today's **2,000,000**" (Pix was at 2,067,960), then out-of-budget until **19:18:56Z** (about 22 min). The cap is now 3M.
- The cap has been raised by hand twice today: 1.67M → 2M → 3M. The first two both made a 10M family cap (×6 desks, then ×5).
- **What counts toward it:** every session that runs on Pix's own row. That is manage (team-lead) sessions, 1:1 chat, meeting replies and facilitation, and host work. They all end in `session.ts` `debit` → `Budget.charge` → `recordUsage`, which adds to `spentTokensToday` (budget.ts:204). Forks' spend also goes onto Pix's `familySpentToday` (budget.ts:209-211).

**2. It blocks work. It is not only a label.** `withinDaily` (budget.ts:248-253) is part of `canStart` (budget.ts:238). That makes it the one gate for:
- **Manager:** in-tray manage sessions (runtime manage.ts:129). A 1:1 during a live session gets only a busy notice (manage.ts:124). Also meeting summaries and replies (meetings.ts:46, :87) and facilitation (meetings.ts:166). So from 18:56 to 19:18Z, Pix could not start manage sessions.
- **Work sessions:** `preflightWork` (work.ts:40-42) refuses the session and sets out-of-budget.
- **The scheduler:** `nextStartable` (domain.ts:113).
- **Forks:** `forkableQueue` returns [] once the family reaches `familyCap` (forks.ts:45). Before 19:18Z the family cap was 10M and the family was at about 9.6M, so the building queue was close to stopping. The manager is also held at the family cap (budget.ts:252).
- **Labels only:** the map status "Out of budget" (overlay.ts:30), the "X today · Y left" line (overlay.ts:53-55, renderer.ts:666), the blockers text (blockers.ts:52-55), the AgentPanel "Today" line and the BuildingPanel "/ agent / day" setting.
- **Soft cap:** a session is charged when it ends (`running` skips the check, budget.ts:312), so one session can overshoot by any amount. The check only stops the *next* start.

**3. It is a leftover the doc never names.** docs/how-work-gets-done.md §8 says "Concurrency = desks; money = free tokens. Nothing else limits exploration." `familyCap` breaks that, because it stops forks, and every exploration fork, at dailyTokensPerAgent × headcount. The §11 build order never mentions `dailyTokensPerAgent` or `familyCap`. The doc's step 3 removed only the exploration allowance and pools, and architecture.md:180 says "the per-agent daily cap is unchanged".

The cap also limits grant and directed work, which free tokens and grant totals already bound. Directed work has no other bound except the balance.

**Recommendation:** delete both caps in the **explore-tick step** (the doc's §11 step 2, queued as as_5il5hk7pji), since that step sets "desks + free tokens" as the only gates. The alternative is a small standalone PR now. Hiding the label just for managers would be wrong: it hides a real hold.

**4. Smallest fix: what to delete**
- **Core**
  - budget.ts:238: drop `this.withinDaily(a, b) &&`.
  - Delete `withinDaily` (budget.ts:243-253).
  - Delete the two `agent-daily` branches in `charge` (budget.ts:319-328) and `"agent-daily"` from `ChargeResult.exhausted` (:15).
  - budget.ts:378: drop the `spentTokensToday < dailyTokensPerAgent` condition.
  - `resumeEligible`/`resetDaily` keep working (they reset to 0 for display).
  - forks.ts:45: drop `|| manager.familySpentToday >= familyCap(b)`.
  - Delete `familyCap` (budget.ts:8-9, forks.ts:10-12, index.ts:40) and `FamilySpend.cap` (forks.ts:263-275, web api.ts:38).
  - blockers.ts:52-55: keep only the "building has no tokens left" and capHold texts.
  - ops.ts:62: comment.
- **Web**
  - overlay.ts:53-55 and renderer.ts:666: show "X today" only.
  - AgentPanel.tsx:262/282: today without a cap.
  - BuildingPanel.tsx:135, :246-249: remove the "/ agent / day" field.
- **Schema:** keep the `dailyTokensPerAgent` column and the zod field (schema index.ts:47, :245, :2115). Nothing reads it after this, the same treatment the pools got.
- **Tests to update:** core budget, forks, caps, schedules, collective-defaults, fork-permissions, bank-adjusted, topic-pages, meeting-context; runtime manage, work, running-debit; web buildingTabs, planDesks, planSideBar.
- **Docs:** architecture.md:37, :174, :180, :265; docs/bank.md:83.

## What I need from you
Decide whether removing the per-agent and family daily caps is fine without a separate Mitchell ask. It changes token policy, which the merge rules say needs asking first, though §8's "capped only by desk capacity and the free tokens" supports it. If yes, add the item 4 deletion list to the explore-tick assignment (as_5il5hk7pji).
