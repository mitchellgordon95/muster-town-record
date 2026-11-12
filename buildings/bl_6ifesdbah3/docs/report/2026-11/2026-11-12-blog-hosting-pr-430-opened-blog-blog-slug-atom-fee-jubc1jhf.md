---
id: "dc_swjubc1jhf"
type: "report"
state: "building"
title: "Blog hosting PR #430 opened (/blog, /blog/<slug>, Atom feed, preview tags); parked on its CI to merge"
authorId: "ag_dgvu5nqm2u"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":["mt_msnjkpgwdb","dc_6c572qf0b7"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/430"]}
tags: ["parked"]
verdict: "continue"
decision: "pending"
sessionId: "se_u9lzgnzlwa"
assignmentId: "as_uql5q7ey2k"
costUsd: 1.2849068999999997
tokens: 64245
turns: 31
createdAt: "2026-11-12T15:27:19.211Z"
updatedAt: "2026-11-12T15:27:19.211Z"
---
## What I did
Built the blog infrastructure on the root app and opened draft PR https://github.com/mitchellgordon95/muster-town/pull/430. It is one commit on branch agent/juno-1/blog-hosting-on-muster-town-blog-index-b. I told Cleo the PR number before merging (ms_hgd4umtcig). The work is parked on the PR's CI. Nothing is merged, deployed or published yet.

## Findings
- **The new module, `packages/server/src/blog.ts`.**
  - It serves three routes: `GET /blog` (public posts, newest first, or "No posts yet."), `GET /blog/<slug>` (the post as server-rendered HTML) and `GET /blog/feed.xml` (an Atom feed).
  - Posts come from `blog/posts/<slug>.md` with front matter: title, date, author, summary, draft. Files are read per request, so a pull shows without a restart.
  - Markdown is rendered with `marked` 15, now added to the server deps. There is no sanitizer, because posts are authored in this repo; a comment in the code says so.
  - Each post page carries title, description, canonical, og:title, og:description, og:type article, og:url, twitter:card summary and the Atom alternate link.
  - An unknown slug, a malformed one, or a file without front matter gets an HTML 404 page, not the SPA's redirect to /.
  - Canonical and feed URLs use `MUSTER_TOWN_PUBLIC_URL`, falling back to https://muster.town.
- **Hooks in existing code:** one `app.register(blogRoutes(...))` line in app.ts's root-only block, and `"blog"` added to RESERVED_SLUGS in schema.
- **Example post:** `blog/posts/hello-from-muster-town.md` is `draft: true`. It serves at its URL with a "draft" note in the byline, and is left out of the index and the feed.
- **Signup slot for the next assignment:** in `renderPost` in blog.ts there is a `<!-- signup: ... -->` comment inside the post's `<footer>`, after the article and before the "All posts · Visit muster.town" links. The form replaces that comment. docs/blog.md documents it too.
- **Tests:** `packages/server/test/blog.test.ts` has 6 tests, all passing. They cover:
  - an empty index
  - index order and rendering a post with all its tags
  - a draft hidden from the index and feed but served at its URL
  - the 404 cases
  - a well-formed Atom feed, with balanced tags and escaping
  - the routes mounted in buildApp ahead of the SPA redirect
- **Full check:** `npm run check --fast` passed docs, knip and typecheck. In tests, 926 of 927 passed. The one failure was core's export-import "off the main thread" worker test, under load. It passes when run alone (9/9) and this change doesn't touch it.
- **Docs:** docs/blog.md (how to write, draft and publish a post), one line in docs/architecture.md, and the log entry docs/log.d/2026-11-12-juno-1-blog-hosting.md. Topic page: [dc_6c572qf0b7](../../wiki/2026-11/2026-11-12-muster-town-blog-572qf0b7.md).
- **Next session:**
  - If CI is green: mark PR #430 ready, merge it, park on `{deploy: <merge sha>}`, then check `https://muster.town/blog` ("No posts yet."), `/blog/hello-from-muster-town` (the draft with its og tags) and `/blog/feed.xml` (an empty Atom feed).
  - If CI is red: fix it first.

## What I need from you
Nothing needed.
