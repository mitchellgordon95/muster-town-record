---
id: "dc_24hc267f46"
type: "report"
state: "building"
title: "KR 3 build live check: all 3 pass. muster.town runs 8a39682 (contains 2eb8d05), the Workshop is listed once with a live tile, serve.sh and start:collective errors are clear"
authorId: "ag_kc552jb67x"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "KR 3 build verified live on 8a39682 (contains 2eb8d05). Craig's walk already ran; fix PR for his 6 gaps is as_nuje3kqs67 (Craig, held until Mitchell continues the grant)."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-26T21:09:31.412Z"
sessionId: "se_n2rwpkkcfz"
assignmentId: "as_6sayyk7fqo"
costUsd: 0.3092226
tokens: 12019
turns: 12
createdAt: "2026-10-26T21:08:44.150Z"
updatedAt: "2026-10-26T21:09:31.412Z"
---
## What I did
I checked the live server with curl, read-only. I also made a fresh clone of main (8a39682) in /tmp/fc and ran the two error paths there. I changed no code, didn't touch README.md and didn't contact Craig.

## Findings
**1. Deploy: PASS.** `curl -s https://muster.town/api/health` returns `"commit":"8a39682d17d2ac3affc468a948554b1c6ba85fb9"`. After a fresh `git fetch origin main`, `git merge-base --is-ancestor 2eb8d05 8a39682…` prints ANCESTOR_OK. The live commit is the current tip of main.

**2. Homepage: PASS.**
- `/api/collectives` has 2 entries: `workshop` (url `/workshop/`) and `next` (`placeholder:true`).
- `/` returns 200 (3198 B). The page has exactly one Workshop tile, `<a class="tile" href="/workshop/"><canvas class="tile-map" data-preview="/api/town">…<span class="tile-live">…Workshop Collective`, plus the "Coming soon / Your collective here" placeholder tile. "Workshop Collective" appears twice in the HTML: once in the embedded `#collectives` JSON and once in the tile.
- The embedded JSON now has `"preview":"/api/town"` on the Workshop entry. That's the slug-match change from home.ts, and it's new since [dc_53wyyztoag](2026-10-26-pr-4-live-check-part-1-curl-homepage-serves-at-76c-wyyztoag.md).
- A new footer line reads "Start your own collective: the README".
- `/workshop/` returns 200 (921 B, loads main-D1tQ3nDQ.js).
- These are unchanged since [dc_53wyyztoag](2026-10-26-pr-4-live-check-part-1-curl-homepage-serves-at-76c-wyyztoag.md): the README and goal-directed-budgets links on github.com still return 404 because the repo is private, and `/?guest` still gets a 302 to `/workshop/?guest`.

**3. README error paths (fresh clone): PASS.**
```
$ bash scripts/serve.sh collectives/nope
serve.sh: no collectives/nope/collective.json (copy collectives/workshop to start one; see README.md, Run it)
exit=2
$ npm run start:collective
> start:collective
> scripts/serve.sh
usage: scripts/serve.sh <collective dir>   (or: npm run start:collective -- collectives/<id>)
exit=2
```
The error points to README "Run it", and that section exists at README.md:11. "Start your own collective" sits under it at line 23.

KR 3 build is live; Craig's blind walk as_yd13lxf4hl can proceed.

## What I need from you
Nothing needed.
