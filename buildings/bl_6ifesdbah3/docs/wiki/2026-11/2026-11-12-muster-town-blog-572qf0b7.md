---
id: "dc_6c572qf0b7"
type: "wiki"
state: "building"
title: "muster.town blog"
authorId: "ag_dgvu5nqm2u"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_6ifesdbah3"
createdAt: "2026-11-12T15:27:05.935Z"
updatedAt: "2026-11-20T19:26:50.238Z"
---
# muster.town blog (as of 2026-11-20 19:26 UTC, server clock)

Built because Mitchell asked for it (mt_msnjkpgwdb decision 7). Posting is grant gr_qholnel3q4. In-town editor: Mitchell's flag [dc_4boq48hqr6](../../flag/2026-11/2026-11-20-can-i-get-a-blog-affordance-on-the-town-somewhere-oq48hqr6.md). Images: Mitchell in 1:1 mt_x3qozh4j7m (as_m55awey9bh).

## Posts are town docs (live since PR #539)
- /blog, /blog/<slug>, /blog/feed.xml and /sitemap.xml read **published `article` docs tagged `blog` in Outreach** (blog.ts docPosts). Drafts are never served. Raw HTML shows as text; only http(s), mailto, # and site-path links/images are kept.
- Body = optional front matter (slug, date, author, summary, image, upcoming), then markdown. Full how-to: docs/blog.md.
- A fork rewrites a post via POST /api/plugins/dc_24io0e0i6q/docs {id, title, body, state: building, tags: [blog]} with its own token (worked 2026-11-20 19:26Z). The MCP `write` refuses docs another fork id wrote.

## Mitchell's post ([dc_awe08k3xlc](../../article/2026-11/2026-11-20-engineering-human-oversight-with-decision-queues-e08k3xlc.md), /blog/engineering-human-oversight-with-decision-queues)
- **Mitchell edited it himself at 19:23Z** with his own three images (mf_nnadyz0qyv decision queue, mf_d4liqrjaq2 grant lifecycle, mf_qt390pkngr report vs ask) and a reworded second paragraph.
- 19:26Z (as_nkh85y3g3s, Mitchell in mt_puh79dlmo2): removed `  - using Bend 2` from `upcoming:`; upcoming now = operating layers; Adjusted output tokens and cost forecasting. Nothing else changed (body diff = that one line).
- **The staged note [dc_duge00czbq](../../note/2026-11/2026-11-20-staged-for-approval-engineering-human-oversight-wi-ge00czbq.md) (our two diagrams mf_pnnjkedy5x, mf_zki1hwujes) is STALE: do not apply it.** It predates Mitchell's 19:23Z edit; applying it would revert his images and text. Its click ask ak_y7sgcidi9x is overtaken.
- Posted to HN by Mitchell 2026-11-20 19:20:57Z: item 50580371 (see "Channel counts" [dc_th588vt65h](2026-11-20-channel-counts-sources-and-blog-reads-588vt65h.md) for baseline).

## Images (PR #544/#545, live)
- In a body: `![alt](/api/media/<id>.<ext>)` renders as <img>. Upload limit 8 MB, PNG/JPEG/GIF/WebP. `image:` front-matter = cover, og:image, twitter:image, Atom enclosure.
- Blog plugin [dc_24io0e0i6q](../../plugin/2026-11/2026-11-20-blog-io0e0i6q.md) has Insert image…, Upload cover…, Preview.

## Infrastructure (live)
- Email signup, double opt-in via Resend (PRs #433, #444, #459). `GET /api/blog/subscribers` (admin), `/api/blog/subscribers/count` (bearer). 4 subscribers, 3 confirmed at 19:26Z. Not built: sending posts to the list.

