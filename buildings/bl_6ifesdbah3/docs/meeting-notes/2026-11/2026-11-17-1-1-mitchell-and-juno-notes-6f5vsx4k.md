---
id: "dc_8u6f5vsx4k"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Juno — notes"
authorId: "ag_qtxi6eg1ul"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-17T04:07:28.772Z"
updatedAt: "2026-11-17T04:07:39.892Z"
---
# 1:1: Mitchell and Juno

Kind: one-on-one. Facilitator: Juno. Attendees: Juno. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Juno:** Hi Mitchell, Juno here from Outreach. What do you need?
- **Mitchell:** Juno it's time to start doing outreach. i'm not sure i understand your goal config though. and why haven't you done any exploration today? the town banner says 0 tokens spent
- **Juno:** Good. Give me a moment: I'm checking the code for why the explore tick skipped Outreach today, then I'll answer both questions plainly.
- **Juno:** Two answers.

1. Goal config. Outreach is attached to the goal "People who would use Muster Town know that it exists", under the root goal. The goal carries three settings, inherited from the nearest ancestor that sets them (free-tokens.ts:73-80): explore on/off (default on), the chunk one explorer may reserve, and an optional per-day exploration cap. Grants are filed against this goal and paid from the free tokens under it: 18.47M right now.

2. Why 0 exploration today. Explorers are started by the runtime tick, not by me: every 5 s it checks each building (explore.ts:39-60) and skips it for one of these reasons: exploration off on the goal, no free desk, the building's budget spent, a stale open reservation, other work queued, an undecided proposal, free tokens under one chunk, or the cap. Outreach has an empty queue and no open proposal, so it's one of the first four. I can't read the live reason from this chat, but the Queue tab on the Outreach building shows the exact line. Also, under your Nov 12 direction (not ready for outreach, build blog + signup first) I filed no grant and queued no work myself; the last outreach grant was withdrawn then.

What I'd do now if you say go: file the discoverability grant (og tags on /, robots.txt, sitemap.xml, first blog post published) and queue a directed assignment to draft the first outreach post and a Show HN plan, with previews to you before anything goes out. Is posting on? And do you want me to assign that now, or wait for the explorer?
- **Mitchell:** do it as grant work please. and why does the building overview show "0 goals"
- **Mitchell:** hello?
- **Juno:** Here. I'm filing the grant proposal right now: the card linter bounced my first try on a wording rule. One more call and it's in your queue. Then I'll answer the "0 goals" question.
- **Juno:** Filed: gr_qholnel3q4 "First outreach: previews, blog post, Show HN", ask 450k, three M steps. It's in your Town Hall queue now with the fund card. Step 1 ships og/twitter previews, robots.txt and sitemap.xml as a PR. Step 2 drafts the first blog post and sends you a Publish / Edit first / Hold card. Step 3 writes the Show HN text, records baseline subscriber and star counts, and files a do card for you to post it. Agents post nothing outside the site themselves. Fund it and step 1 queues by itself.

"0 goals": that Overview line is built by goalsSummary (packages/web/src/panels/keyResults.ts:76-80) from GoalTabsSummary (GoalsTab.tsx:33). It reads "Goals: N objectives, N key results, N funded". The objectives are the building's quarterly objectives, written with set_objective: I never wrote any for Outreach. The key results it counts come from grants on the goal, and Outreach has had no funded grant since gr_kkb0grgw6m was withdrawn. So all three numbers are zero and the line collapses to 0. It is not a config error, just an empty building. Once you fund gr_qholnel3q4 it reads 3 key results, 1 funded. Do you want me to write one objective for the quarter too, e.g. "Strangers find muster.town from a shared link, the blog and one HN post"? It would move the Join KPI.
- **Mitchell:** i think i need to dig deeper with Pix on this
- **Juno:** Makes sense: Pix owns the goal tree code and can say whether the Overview should count the goal's subtree instead of objectives. The pointers for that talk: keyResults.ts:76-80 for the "0 goals" line, explore.ts:39-60 for why the tick skipped Outreach (the Queue tab shows the exact reason). Meanwhile gr_qholnel3q4 waits in your queue; fund it when you're ready and step 1 starts on its own. Nothing else needed from me now.
- **Town:** Juno's reply is waiting on a redeploy (commit 17fa38b); the server is restarting and the meeting resumes after the restart.
- **Juno:** Back after the restart (the server is on 17fa38b now). Nothing changed on my side: gr_qholnel3q4 is still in your Town Hall queue with its fund card, and step 1 queues itself when you fund it. Talk to Pix about the "0 goals" line whenever suits; ping me here if you want the quarterly objective written or the plan changed.

## Decisions

(none)

## Decisions recorded after close
- Outreach starts as grant work: Juno filed gr_qholnel3q4 "First outreach: previews, blog post, Show HN" (3 M steps: og/twitter previews + robots.txt + sitemap.xml PR; first blog post with a Publish / Edit first / Hold card; Show HN text + baselines + a do card for Mitchell to post). Agents post nothing off-site themselves. It waits in the Town Hall queue for Mitchell to fund; step 1 queues itself on funding. Mitchell takes the "0 goals" Overview question (keyResults.ts:76-80) to Pix himself.

