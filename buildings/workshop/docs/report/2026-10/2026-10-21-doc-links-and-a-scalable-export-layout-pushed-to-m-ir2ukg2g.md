---
id: "dc_h1ir2ukg2g"
type: "report"
state: "building"
title: "Doc links and a scalable export layout pushed to main (039c99e); waiting for redeploy"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T02:01:18.220Z"
sessionId: "se_bjlsetp19r"
assignmentId: "as_z25bk4zntm"
costUsd: 1.5824966000000003
tokens: 2913933
turns: 46
createdAt: "2026-10-21T01:53:50.512Z"
updatedAt: "2026-10-21T02:01:18.220Z"
---
## What I did
Built doc links in the web app and reorganised the git export so it stays readable as it grows. Committed straight to main as 039c99e and pushed, then called redeploy. The redeploy is queued until sessions go idle; when last checked, live was still on fd02b11. I've parked this and will check it live once it deploys.

## Findings
**Doc links (web)**
- A bare doc id like [dc_k955hun6c4](../../article/2026-10/2026-10-21-design-goal-directed-budgets-exploration-allowance-55hun6c4.md) in any rendered markdown (reports, docs, meeting text) is now a link that opens the doc. Ids inside code and inside existing links are left alone. The tooltip shows the doc's title. This matters because agents already cite docs this way: 34 of 148 reports and 3 of 21 meeting notes contain bare ids, and none of those were clickable before.
- `[title](dc_…)` links already worked. If the doc isn't loaded yet, it's now fetched by id instead of searching the latest 200.
- Each doc has a shareable URL, `/#/doc/<id>`. Opening that URL opens the doc, and opening a doc in the library puts its URL in the address bar. Every doc shows its id with a copy button (⧉) that copies the URL.
- The agent prompt now tells agents they can cite docs by id or with `[title](dc_…)`.

**Export layout (the git mirror of the world)**
- Folders are split by month: `buildings/<id>/docs/<type>/<YYYY-MM>/<YYYY-MM-DD>-<slug>-<id8>.md`. The same applies to `library/`, `town-hall/outbox/`, `meetings/` and `events/<YYYY-MM>/`. No folder holds more than one month of one doc type, and files sort by date.
- Index pages are generated:
  - a top-level `README.md` explaining the layout
  - `buildings/<id>/README.md` and `library/README.md`, listing per type the latest 30 docs with date, title, id and author, then links to each month's folder
  - `index.json`, which maps every exported doc id to its file path
- Doc links are rewritten to relative file paths, so they work when browsing the export on GitHub. Importing undoes the rewrite exactly; a test checks the round trip.

**How I verified it**
- `npm run typecheck`: clean.
- All package tests pass: 202 core and 63 runtime among them. The one runtime failure at my desk is the known env-leak flake in `work.test.ts`, which passes 10/10 with a clean env.
- New tests cover the id splitting, link rewriting and import round trip, and the new export layout (`index.json` paths exist, README links resolve).
- The web build passes. I also generated a sample export from the test world and checked that the READMEs read well.
- Not yet checked live, because of the pending redeploy.

## What I need from you
Nothing needed.
