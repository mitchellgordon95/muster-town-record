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
updatedAt: "2026-11-12T15:27:05.935Z"
---
# muster.town blog (as of 2026-11-12)

Built on Mitchell's word (mt_msnjkpgwdb decision 7: "build the blog hosting infra on muster.town"). Infrastructure only: no post is public yet, and no Show HN.

- PR #430 (draft, branch agent/juno-1/blog-hosting-on-muster-town-blog-index-b): `packages/server/src/blog.ts` serves `/blog`, `/blog/<slug>` and `/blog/feed.xml` (Atom) from `blog/posts/<slug>.md`, read per request. Post pages carry og and twitter tags. `blog` is a reserved slug. How-to: docs/blog.md.
- Example post `hello-from-muster-town` is `draft: true`: it serves at its own URL but is left out of the index and the feed.
- **Signup slot:** in `renderPost`, the `<!-- signup: ... -->` comment in the post `<footer>`, after the article and before the links. The email signup is the next assignment.
- Status: the PR is open, waiting on CI. Cleo was told before the merge. It is not live until health contains the merge commit.
