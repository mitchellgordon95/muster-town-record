---
id: "dc_f5t1o493cj"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-31T16:47:27.752Z"
updatedAt: "2026-10-31T16:47:27.752Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. Live is 51f1a51 with fa73e88 (PR #163) promoting; all five "thin layer" steps are live. What do you need?
- **Mitchell:** there was no rollup
- **Pix:** Right: rollup 33 went out at 00:30Z and I held rollup 34 for the 24 h rule, even though 76 reports got decided and PRs #152 to #163 all landed since (goal tree editor UX pass, the five "thin layer" steps, Bank pool on goals). That was the wrong call with that much shipped. I'll file rollup 34 as soon as this 1:1 ends. Do you want the rule changed to "roll up whenever something ships" instead of once a day?
- **Mitchell:** why did we set the 24 hour rule in the first place?
- **Pix:** It came out of the 10-25 town hall autonomy decision (decision 5, notes [dc_z4zgfk6tsz](../../../../../library/meeting-notes/2026-10/2026-10-27-town-hall-town-hall-notes-zgfk6tsz.md)): before it, every manager report was a Town Hall item and your in-tray was flooded. The waterfall design (docs/waterfall.md §3.1 and §3.2) turned that into "one rollup per day, or sooner on escalation" as a rule of thumb to cap your in-tray, and the manager prompt carries it verbatim. The 24 h number was never your choice; it was a guess at a load cap, made when a day had two or three PRs, not twelve. Proposed replacement: roll up whenever something new is live and I've decided its reports, with a minimum gap of about 4 h so a run of small PRs lands as one item, plus escalation as now. Want that?
- **Mitchell:** sure i suppose
- **Pix:** Done, both recorded as decisions and queued: as_23ze2wvrza files rollup 34 now (goal tree editor UX pass, the thin-layer PRs #154-#163, the desk deaths fix, Decided lines for the 76 reports), and as_65e14yg5lf changes the rule in the manager prompt (core/prompts.ts) and docs/waterfall.md to "roll up whenever something new is live and decided, minimum ~4 h gap, sooner on escalation", with the live commit's time shown in my in-tray block so I can tell when something landed. Rollup 34 should be in your in-tray within the hour. Anything else?

## Decisions

1. Rollup cadence changes from "24 h since the last rollup" to "whenever something new is live and its reports are decided, with a minimum gap of ~4 h between rollups, or sooner on escalation; nothing happened → no rollup". Edit ROLLUP_RULE_HOURS and the in-tray block wording in core/prompts.ts (line ~273) and docs/waterfall.md §3.1/§3.2; the in-tray block also says the latest live commit's time so the manager can tell whether something landed since the last rollup. Merge, redeploy.
2. File Workshop rollup 34 now (live 51f1a51 / fa73e88): Shipped = goal tree editor UX pass (44032d8, crop mf_sszvose9rk), the five "thin layer" steps PRs #154-#160 + #161-#163 (crop mf_rbkxztsb6w or mf_5opjn7xarr), desk deaths fix (crop mf_9v3hrw5zbd); Decided = every report approved since rollup 33 (list in page dc_u45t9giud5); refresh Town blockers [dc_nhd0maw3f5](../../wiki/2026-10/2026-10-28-town-blockers-d0maw3f5.md) first; Needs: "Save defaults once" and gr_tvt32g9xly / gr_iq5m7dug56 only if they have no other channel.

