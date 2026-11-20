---
id: "dc_m7r3yftq2x"
type: "report"
state: "building"
title: "Blog plugin installed live; /blog moves to town docs in PR #539, parked to merge when green"
authorId: "ag_dypyd3mo6g"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-20T02:38:11.556Z"
sessionId: "se_z06jxs6u3z"
assignmentId: "as_up3y7heihf"
costUsd: 2.9290850999999996
tokens: 146454
turns: 64
createdAt: "2026-11-20T02:38:11.551Z"
updatedAt: "2026-11-20T02:38:11.556Z"
---
## What I did
- Confirmed #536 is live: /api/health showed b71d6025 from 02:30:31Z.
- Installed both plugins in Outreach: **Notes** [dc_lhdyryo2jm](../../plugin/2026-11/2026-11-20-notes-dyryo2jm.md) and **Blog** [dc_24io0e0i6q](../../plugin/2026-11/2026-11-20-blog-io0e0i6q.md).
- Built the Blog plugin page (`docs/plugins/blog.plugin.html`).
- Moved /blog onto town docs in PR https://github.com/mitchellgordon95/muster-town/pull/539.
- Moved Mitchell's post into doc [dc_awe08k3xlc](../../article/2026-11/2026-11-20-engineering-human-oversight-with-decision-queues-e08k3xlc.md).
- Updated docs/blog.md, docs/plugins.md, docs/architecture.md and the topic pages [dc_6c572qf0b7](../../wiki/2026-11/2026-11-12-muster-town-blog-572qf0b7.md) and [dc_8an7b5hviv](../../wiki/2026-11/2026-11-20-town-plugins-n7b5hviv.md).

## Findings
- **Outreach back wall (live now).** There are two screens, at places plugin:dc_lhdyryo2jm (Notes) and plugin:dc_24io0e0i6q (Blog). GET /api/plugins?buildingId=bl_6ifesdbah3 lists both.
  - The Blog screen lists the published posts and the viewer's drafts. It opens a post into a form: title, slug, date, author, summary, coming-next lines and markdown. It then saves a draft or publishes.
  - Unpublish is shown only to a post's author, because a draft is private and would vanish for everyone else.
  - Mitchell, as admin, can edit any published post.
- **Live route checks.** POST /api/plugins/:id/docs wrote a draft note (dc_r690u0mt5n) and a blog draft (dc_ioysds2wir, slug draft-check). Both are private to me and owned by their plugins. Listing works on both plugins.
- **Page script check.** I ran the Blog page in headless Chromium against a fake bridge. Opening and saving Mitchell's post sends back a byte-identical body. A new post saves as front matter plus markdown, with the slug fixed at the first save.
- **Not checked:** the iframe sheet in a real browser on the live town. Headless Chromium stayed at "Entering town…".
- **PR #539 (/blog from docs).** /blog, /blog/<slug>, /blog/feed.xml and /sitemap.xml read published `article`s tagged `blog` in Outreach (`blog.ts` `docPosts`/`postOf`). The PR deletes blog/posts/*.md.
  - Drafts are never served. Before, a draft was served at its URL; now it is private and gets a 404.
  - Posts are no longer trusted repo files. So raw HTML in a post shows as text, and only http(s), mailto and site-path links are kept. Mitchell's post renders to the same HTML as before.
  - Tests: blog.test.ts rewritten on docs (13 tests), plus new cases for building, tag and type filters, duplicate slugs and the XSS cases. `npm run check --fast` passed.
- **URLs after #539 deploys.** These stay the same: https://muster.town/blog and https://muster.town/blog/engineering-human-oversight-with-decision-queues (doc [dc_awe08k3xlc](../../article/2026-11/2026-11-20-engineering-human-oversight-with-decision-queues-e08k3xlc.md), published, body identical to the file). The placeholder draft hello-from-muster-town was dropped; it was never public.
- **Left out.**
  - No live check of /blog after #539 deploys: parking on merge closes this work with no new session. The check is: /blog lists the post, the post URL, feed and sitemap work, and /blog/draft-check gives 404. It is a small job.
  - The two test drafts stay as my private drafts.
  - Posts are not yet sent to the mailing list.

## What I need from you
Nothing needed.
