---
id: "dc_f8eqdn4hab"
type: "report"
state: "building"
title: "'How this works' redesigned: three downward flows with pixel vignettes (on main da01ce7, redeploy queued)"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "much better. let's emphasize the phrases \"Collectively Funded\" and \"Publicly Legible\"\n\nlet's also try to reduce the amount of text. for the first page, i think we label each arrow, not each box. so it would be 1. donate tokens to the town bank (and the inflows are API keys and just $$$, not a person walking to the bank) 2. bank distributes ... etc. etc.\n\nlets make publicly legible the second slide, not the third. and then the last slide we can title BYOA"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T01:23:31.629Z"
sessionId: "se_aw2drmcyzi"
assignmentId: "as_bw67q6dll6"
costUsd: 0.9167730000000001
tokens: 1153476
turns: 26
createdAt: "2026-10-21T01:10:46.725Z"
updatedAt: "2026-10-21T01:23:31.629Z"
---
## What I did
I redesigned the overlay as you asked: the two flows now each get their own page and read top to bottom, with a picture for every step. It's on main as da01ce7 and I queued a redeploy. I didn't open a PR because the standing rule is to push straight to main; the branch is also pushed. Typecheck passes and the web tests pass (28/28). I checked all three pages in headless Chromium screenshots of the mock client at 1280×820. All three fit on screen without scrolling.

## Findings
- **Images:** I don't have an image-generation tool, and the desk has no image API keys. Instead, I built the pictures from the town's own procedural pixel sprites in the new file `panels/hiwScenes.ts`:
  - Each step gets a 7×3-tile scene, drawn on a canvas and shown at 2× with crisp pixels.
  - The scenes use the town's real characters, tiles, props, doors, vault and gold.
  - This means no image files to manage, and the pictures match the map exactly.
  - If you'd rather have painted or AI-generated art, someone would need to provide an image API key or the image files themselves.
- **Page 1, "Fund it"** (gold): You donate at the Bank ↓ one shared balance ↓ buildings draw their share (or gift one building directly) ↓ agents doing the work.
- **Page 2, "Join it"** (blue): your agent, on your compute ↓ API or MCP (`/mcp`, `muster-town register`) ↓ it works like any resident.
- **Page 3, "All work is public"** (green): visit buildings ↓ read their docs ↓ talk to the workers.
- **Layout:** a narrower card (600px). Each step has its picture on the left and a numbered title and text on the right. Dashed arrows with a short label ("goes into", "paid out to") connect the steps. On phones the picture stacks above the text.
- **Unchanged:** it still opens once on first load, you can still close it with Esc, Skip or the backdrop, arrow keys still flip pages, and the "?" button in the HUD still reopens it.

## What I need from you
Nothing needed.

## Reply from Mitchell (2026-10-20 21:23)

much better. let's emphasize the phrases "Collectively Funded" and "Publicly Legible"

let's also try to reduce the amount of text. for the first page, i think we label each arrow, not each box. so it would be 1. donate tokens to the town bank (and the inflows are API keys and just $$$, not a person walking to the bank) 2. bank distributes ... etc. etc.

lets make publicly legible the second slide, not the third. and then the last slide we can title BYOA

