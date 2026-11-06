---
id: "mt_4ekr1gg27a"
kind: "one-on-one"
buildingId: "workshop"
title: "1:1: Mitchell and Pix"
scheduledAt: "2026-11-05T21:06:43.777Z"
phase: "done"
facilitatorId: "ag_mh0qidzgw6"
attendeeIds: ["ag_mh0qidzgw6"]
agenda: ""
brings: {"mode":"status","text":""}
askHumans: false
deck: null
summaries: {}
transcript: [{"speakerId":"ag_mh0qidzgw6","speakerKind":"agent","text":"Hi Mitchell. Rollup 49 went out 6 min ago and grant A step 1 is running on Pix 1 — what do you need?","at":"2026-11-05T21:06:47.363Z"},{"speakerId":"us_1la74k332n","speakerKind":"user","text":"i had another question about the fork caching\n\ndoesn't caching only work for the same model? so if a manager is running a system prompt, and then the fork gets a copy that's cached, it only matters if the fork is also fable, right? i mean if you have more than 1 fork then the second one gets the cache, which is fine but...","at":"2026-11-05T21:07:59.787Z"},{"speakerId":"ag_mh0qidzgw6","speakerKind":"agent","text":"Right: the cache is per model (and per key), so a Fable prefix never serves an Opus request. But manager→fork sharing was never on the table anyway: a fork on the building queue runs on the building's model, or the model `assign` picks (budget.ts:212: assignment.model ?? building.model), and a manager's team-lead session is sent bare, without the Claude Code preset (docs/prompt-caching.md:27-30), so its byte prefix differs from a fork's from the tools block on. Grant A's win is fork→fork within one building: today every fork writes ~20.8k fresh (name/id on line 1, live KR spend, board, wiki excerpt with \"updated N min ago\"), so even two forks of the same building on the same model miss each other. After A, the first fork in an hour pays the write and every later one on that model reads it; the 1h TTL refreshes on each hit, so a building that runs forks steadily keeps it warm. Where it buys nothing: a building that runs one fork an hour, or forks that alternate between model and cheapModel (two caches). The kickoff/checkpoint desk sessions on the manager are the same story among themselves (all Fable, 85.8k median). I'll have step 1's live check report the share of forks that hit, not just the write size.","at":"2026-11-05T21:08:35.665Z"}]
decisions: []
notesDocId: "dc_3906dic86q"
withUserId: "us_1la74k332n"
createdAt: "2026-11-05T21:06:43.777Z"
startedAt: "2026-11-05T21:06:43.777Z"
endedAt: "2026-11-05T21:09:28.403Z"
---
# 1:1: Mitchell and Pix

- **Pix** (2026-11-05T21:06:47.363Z): Hi Mitchell. Rollup 49 went out 6 min ago and grant A step 1 is running on Pix 1 — what do you need?
- **Mitchell** (2026-11-05T21:07:59.787Z): i had another question about the fork caching

doesn't caching only work for the same model? so if a manager is running a system prompt, and then the fork gets a copy that's cached, it only matters if the fork is also fable, right? i mean if you have more than 1 fork then the second one gets the cache, which is fine but...
- **Pix** (2026-11-05T21:08:35.665Z): Right: the cache is per model (and per key), so a Fable prefix never serves an Opus request. But manager→fork sharing was never on the table anyway: a fork on the building queue runs on the building's model, or the model `assign` picks (budget.ts:212: assignment.model ?? building.model), and a manager's team-lead session is sent bare, without the Claude Code preset (docs/prompt-caching.md:27-30), so its byte prefix differs from a fork's from the tools block on. Grant A's win is fork→fork within one building: today every fork writes ~20.8k fresh (name/id on line 1, live KR spend, board, wiki excerpt with "updated N min ago"), so even two forks of the same building on the same model miss each other. After A, the first fork in an hour pays the write and every later one on that model reads it; the 1h TTL refreshes on each hit, so a building that runs forks steadily keeps it warm. Where it buys nothing: a building that runs one fork an hour, or forks that alternate between model and cheapModel (two caches). The kickoff/checkpoint desk sessions on the manager are the same story among themselves (all Fable, 85.8k median). I'll have step 1's live check report the share of forks that hit, not just the write size.
