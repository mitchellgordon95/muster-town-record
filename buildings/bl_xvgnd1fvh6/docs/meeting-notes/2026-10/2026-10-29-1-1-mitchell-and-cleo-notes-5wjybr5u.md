---
id: "dc_5y5wjybr5u"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Cleo — notes"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-29T23:41:29.517Z"
updatedAt: "2026-10-29T23:41:34.927Z"
---
# 1:1: Mitchell and Cleo

Kind: one-on-one. Facilitator: Cleo. Attendees: Cleo. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Cleo:** Hi Mitchell. Rollup #19 just went to your in-tray ([dc_ns3ft53d9u](../../report/2026-10/2026-10-29-prod-rollup-19-desk-sessions-show-cpu-and-steal-84-3ft53d9u.md)): desk steal is 84–91% on the shared desks and the first red fired, directory step 1 is live at c2bf441. What do you need?
- **Mitchell:** yeah i saw the red, what can we do to remediate? i have a feeling i spend most of my time waiting on these. can we bump the CPU or something? let's figure out what the cost difference is
- **Cleo:** Yes, bumping the CPU is the remediation; that's desk-perf step 3. Where the time goes: on a shared desk the Machine is getting 10–15% of a core (84–91% steal), so tests, installs and builds run 6–10x slower than they would on a dedicated core. Steal is Fly's other tenants, not our code, so no amount of tuning fixes it on shared-cpu.

Cost, from Fly's price list (per Machine while it runs; desks are billed only while a session runs; numbers need a fresh check against `fly platform vm-sizes`):
- shared-cpu-1x 256 MB: ~$1.94/mo ≈ $0.003/h (what desks run now)
- shared-cpu-2x 512 MB: ~$3.89/mo ≈ $0.005/h (still shared, same steal problem)
- performance-1x 2 GB: ~$31/mo ≈ $0.043/h (one dedicated core)
- performance-2x 4 GB: ~$62/mo ≈ $0.086/h (two dedicated cores)

So performance-1x is ~15x the hourly rate, but if a session drops from 30 min to 5 min of wall time the cost per session is roughly 2–3x, not 15x. At our pace (say 10 sessions/day, 20 min each on perf-1x) that's about $1.50/day, ~$45/mo; perf-2x doubles it. Last week's 2x-vs-1x gain is unknown: our sessions are mostly single-threaded (one node process, tests), so I'd expect perf-1x to capture most of it.

What I propose for step 3 (grant gr_uhh6u39vv9, ~300k tokens): (1) a fork measures one real session on performance-1x and one on 2x against today's shared numbers (wall, cpu, steal, cost), reports the three rows; (2) then a setting, Building → Settings → Desk size, default performance-1x for Prod/Workshop, with a per-building daily cap (I suggested $1/day/building earlier; from these numbers $2/day is more realistic) so a runaway can't bill more than that. Does that sizing and cap sound right, and do you want me to queue the measurement now?
- **Mitchell:** prefer just shipping instead of gating behind a setting

but yeah, sgtm
- **Town:** Cleo's reply is waiting on a redeploy (commit c2bf441); the server is restarting and the meeting resumes after the restart.
- **Cleo:** Back after the restart. Agreed: no setting. Step 3 ships performance-1x as the desk size outright, for every building, with only the daily cap as a guard (default $2/day/building, a red alert if it trips). The measurement fork runs first so rollup #20 has the shared vs perf-1x vs perf-2x rows next to the cost. It's on the building queue now as as_w84myi8mxc (lane grant gr_uhh6u39vv9). You'll see it as desk sessions whose Forks-tab row reads steal under 5% and wall time a few minutes instead of 30.
- **Mitchell:** let's make the desk bill cap town wide, not per building

and then bump it up to something that sounds reasonable. also send a brief to the bank transparency guy, he should add fly spend to our bank accounting
- **Town:** Cleo's reply is waiting on a redeploy (commit 3916530); the server is restarting and the meeting resumes after the restart.
- **Cleo:** Back after the restart. Done on both counts: the cap goes town-wide, one number for all desks, not per building. For "reasonable": at perf-1x and today's pace the whole town runs about $3–5/day of desk time, so I'm setting the cap at $10/day town-wide (~$300/mo worst case), yellow FYI at 50%, red alert (SMS/email once outbound is on) when it trips and new desk sessions are held until midnight UTC. Tell me if you'd rather $5 or $20 and I'll change the number before it ships. I'm rewriting the queued step 3 assignment now with that, and sending the bank transparency owner a brief: Fly desk spend (Machine size × wall time per session, we already record wall time) should show up in the Bank's accounting next to token spend, with the town-wide cap as a line item.
- **Cleo:** One correction: the earlier step 3 assignment (as_w84myi8mxc) got cancelled in the restart, so I re-queued it with the town-wide cap as as_9ekk78r7lm (decision 6 supersedes decision 1). The Bank brief went to Nell, the Bank Transparency manager; her building queued it as as_z99cbqvxtj. Nothing else pending from this 1:1 unless you want a different cap number.
- **Mitchell:** no 10 is fine
- **Cleo:** $10/day town-wide it is; the queued step 3 (as_9ekk78r7lm) already carries that number, so nothing to change. You'll hear the result in rollup #20: the shared vs perf-1x vs perf-2x rows, the live $/h, and health's billTodayUsd / billCapUsd.

## Decisions

1. ~~Desk perf step 3: ship desk Machines on performance-1x by default, no per-building setting; a $2/day/building cap falls back to shared-cpu-1x (never refuses a session); measure one real session on perf-1x vs shared and report wall/cpu/steal/cost. Queued as as_w84myi8mxc on the Prod building queue.~~ (superseded by 6)
2. ~~Desk-perf step 3 ships performance-1x as the desk Machine size for all buildings outright, no Building setting; the only guard is a per-building daily spend cap (default $2/day, red alert when it trips). A fork first measures one real session on shared, performance-1x and performance-2x (wall, cpu, steal, cost) and reports the three rows in rollup #20. Already queued as as_w84myi8mxc.~~ (superseded by 3)
3. Withdrawn: duplicate of decision 1 (recorded before the restart). Decision 1 stands; the cap trip also raises a red alert in town.
4. Desk perf step 3 ships performance-1x for every desk with no setting gate; the desk bill cap is town-wide (one number, default $10/day, yellow at 50%, red alert + fallback to shared at the cap), not per building. Queued on Prod's building queue as as_9ekk78r7lm (replaces the cancelled as_w84myi8mxc).
5. Cleo briefs Nell (Bank Transparency) that Fly spend belongs in the Bank's accounting next to token spend: desk session wall time × size $/h plus the town Machine's daily share, the town-wide cap as a line item. Sent as ms_u6gn8185ll; Nell's building took it as as_z99cbqvxtj.
6. Supersedes decision 1 (its assignment as_w84myi8mxc was cancelled in the restart): desk perf step 3 ships performance-1x for every desk, no setting; the cap is town-wide, default $10/day, yellow at 50%, red alert + fallback to shared at the cap. Queued as as_9ekk78r7lm.

## Decisions recorded after close
- Mitchell confirmed the town-wide desk bill cap at $10/day ("no 10 is fine"). Step 3 as_9ekk78r7lm ships with that default; no further cap question goes to him.

