---
id: "dc_uhli9tptwx"
type: "report"
state: "building"
title: "Outreach rollup #3: blog hosting is live on muster.town (/blog, posts from markdown in the repo, Atom feed); email signup is next"
authorId: "ag_qtxi6eg1ul"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":["dc_e77f0rraxy","dc_swjubc1jhf","dc_xr0zl1z4sa","dc_nlb86kmehq"],"urls":["https://muster.town/blog","https://muster.town/blog/hello-from-muster-town","https://muster.town/blog/feed.xml","https://github.com/mitchellgordon95/muster-town/pull/430"]}
tags: ["rollup","untyped-asks"]
verdict: "continue"
decision: "pending"
sessionId: "se_lym2akbt2s"
createdAt: "2026-11-12T16:04:31.690Z"
updatedAt: "2026-11-12T16:04:31.690Z"
---
Live: 7c182fe (contains 192ace07, PR #430). You said in your 1:1 with Secretary (mt_msnjkpgwdb): not ready to post yet, build the blog hosting on muster.town, with an email signup at the foot of each post. The first half is live; the signup is on the queue.

## Shipped

**1. muster.town has a blog: /blog, one page per post, and an Atom feed**

**What it is:** Posts are markdown files in the repo (blog/posts/<slug>.md with title, date, author, summary and a draft flag). The server renders /blog, /blog/<slug> and /blog/feed.xml, with the preview tags a link needs on Twitter, Slack or Discord. A draft post is reachable by its URL but kept off the index and the feed, so you can preview before you publish. Publishing a post is flipping draft to false and merging. PR #430 merged as 192ace07; reports [dc_swjubc1jhf](2026-11-12-blog-hosting-pr-430-opened-blog-blog-slug-atom-fee-jubc1jhf.md), [dc_xr0zl1z4sa](2026-11-12-blog-hosting-pr-430-merged-as-192ace07-parked-unti-0zl1z4sa.md), [dc_nlb86kmehq](2026-11-12-blog-hosting-is-live-on-muster-town-blog-the-draft-b86kmehq.md); how-to in docs/blog.md.

**What you'd see:** https://muster.town/blog says "No posts yet." (the only post is a draft). https://muster.town/blog/hello-from-muster-town shows the draft placeholder post with the signup slot at its foot. https://muster.town/blog/feed.xml is a valid, empty Atom feed. No picture this time: the pages are one click away at those URLs.

**Your call:** The signup form that comes next stores an address with no confirmation email, because the town has no mail sender. Tell Juno if you want double opt-in instead; otherwise it ships as a plain input.

## Decided
- [dc_e77f0rraxy](2026-11-12-message-from-mitchell-via-secretary-from-mitchell-7f0rraxy.md) → approve (your direction relayed by Secretary: blog hosting and signup queued, gr_kkb0grgw6m withdrawn)
- [dc_swjubc1jhf](2026-11-12-blog-hosting-pr-430-opened-blog-blog-slug-atom-fee-jubc1jhf.md) → approve (PR #430 opened, parked on CI)
- [dc_xr0zl1z4sa](2026-11-12-blog-hosting-pr-430-merged-as-192ace07-parked-unti-0zl1z4sa.md) → approve (PR #430 merged as 192ace07, parked until live)
- [dc_nlb86kmehq](2026-11-12-blog-hosting-is-live-on-muster-town-blog-the-draft-b86kmehq.md) → approve (blog verified live at 7c182fe; signup assignment follows)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| (none funded) | — | — | — |

Spend today by lane: exploration 0 tokens; directed 78,866 tokens (the blog hosting chain). Free under the goal: 14,719,319. On the queue: as_k1oe6hzp3d, the email signup (directed, your 1:1 with Secretary).

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 0 proposals, 0 requests, 1 rollup ([dc_e4k903km69](2026-11-05-outreach-rollup-2-the-repo-is-mit-licensed-pr-366-k903km69.md))._
