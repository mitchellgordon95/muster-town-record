---
id: "dc_i2ln43k253"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Nell — notes"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-30T20:05:55.845Z"
updatedAt: "2026-10-30T20:05:55.845Z"
---
# 1:1: Mitchell and Nell

Kind: one-on-one. Facilitator: Nell. Attendees: Nell. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Nell:** Hi Mitchell. The one Bank page is live at f402bcf with Teo's tabs, all four finance key results are met, and nothing is queued. What do you need?
- **Mitchell:** queue some work for me. after core does the big goal and bank refactor

right now there's no explanation for how we compute adjusted output tokens. the only way to know the percentages there is by looking at real usage. so i think the bank has a single estimate that's easily visible about what an adjusted token is (x% input, y% cache reads, etc.)

and we update that... daily? based on our token usage logs. and that global number is actively used any time we use or show adjusted output tokens?
- **Nell:** Got it. Here's what I'd queue, as one directed assignment under this 1:1, held until Core's refactor lands:

1. One global "adjusted token mix" record in the Bank: the formula plus the current percentages (x% input, y% cache read, z% cache write, w% output), with the date it was last computed and the window it came from.
2. A daily recompute from the usage logs (say the trailing 7 days), stored in the DB so the number survives restarts; first run back-fills from existing logs.
3. Every place that converts raw usage to adjusted tokens or shows adjusted tokens reads that one global number, so no hardcoded weights remain.
4. Visible on the Bank page's Tokens tab, one line with the breakdown and an "updated daily" note, and in the three finance endpoints so check:finance can assert used + remaining still holds.

I'd also add it as a new key result on the building goal ("Anyone can see what an adjusted token is and the mix behind it") so it can carry a grant later; you can cut it from the rollup if you'd rather not.

One question: how should the hold work? If you have Core's assignment id I'll use waitFor on it; otherwise I'll queue it waiting on the next redeploy and tell the fork to rebase on whatever the Bank refactor shipped.
- **Mitchell:** we're changing how grants work, maybe just schedule a cron for tomorrow night
- **Nell:** Done: scheduled sc_p5oj6u7pks, one shot, fires 2026-11-01 02:00Z (tomorrow 7pm Pacific). It creates a directed assignment on my queue under this 1:1 and a fork of me runs it: find the current adjusted-token formula, store one global mix record (input / cache read / cache write / output percentages over the trailing 7 days, with computedAt), recompute it daily from the usage logs, make every adjusted-token computation and display read that record, and show one plain line on the Bank's Tokens tab. The fork starts by reading what Core's refactor changed on main and stops rather than builds if the refactor is still half-landed. No key result or grant, since grants are changing. If a different time suits better, say so and I'll move it.

## Decisions

(none)
