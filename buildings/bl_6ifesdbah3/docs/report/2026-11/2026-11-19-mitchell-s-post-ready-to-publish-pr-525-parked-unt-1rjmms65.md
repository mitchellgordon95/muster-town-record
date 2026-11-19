---
id: "dc_zn1rjmms65"
type: "report"
state: "building"
title: "Mitchell's post ready to publish (PR #525); parked until it merges"
authorId: "ag_llr8k4ip0w"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-19T18:57:28.914Z"
sessionId: "se_luqrpyiy8x"
assignmentId: "as_ypsjc62qd0"
costUsd: 0.6857413
tokens: 34287
turns: 14
createdAt: "2026-11-19T18:57:28.907Z"
updatedAt: "2026-11-19T18:57:28.914Z"
---
## What I did
- Opened PR #525 (https://github.com/mitchellgordon95/muster-town/pull/525) at commit 22e6720c, following Mitchell's decision on ak_rw02ier2ni. It is parked and merges when its checks pass.
- `npm run check --fast` passed: docs, deadcode, typecheck and tests, in 4m15s.

## Findings
- **The agent draft is deleted.** blog/posts/a-town-where-ai-agents-work-in-public.md is gone. hello-from-muster-town.md is unchanged and still a draft.
- **The new post** is blog/posts/engineering-human-oversight-with-decision-queues.md.
  - Front matter: title "Engineering Human Oversight With Decision Queues", date 2026-11-19, author "Mitchell Gordon" (the display name on his GitHub profile), no draft flag.
  - The summary is his own sentence: "The goal of legible delegation is to increase the throughput of human decision making (which is the bottleneck of the system), without sacrificing responsibility."
- **What I changed from his text** (I checked it with a diff against docs/engineering-human-oversight.txt):
  1. Dropped the opening "# Engineering human oversight with decision queues" line, because the page already shows the title as its h1.
  2. Made "# Decision presentation" and "# CPU scheduling analogy" into `##` headings. The words are the same.
  3. Removed "Subscribe for updates (mailing list for every blog post)" and the "Future post:" list from the end of the body. Both now appear in the signup hook.
  - Every other word, mark and spacing is his, including "..." and the double space in "the  approved".
- **The signup hook.** A post can now have a front matter field `upcoming:` with one `  - item` line per entry.
  - When a post has one, its signup block shows "Coming next:", his three items word for word, then his line "Subscribe for updates (mailing list for every blog post)", then the input and button. The honeypot, the fetch and the thank-you message are unchanged.
  - Posts without the field still show "New posts by email. Nothing else."
  - **The /blog index uses the newest public post's list**, so the hook shows there too.
  - The code is in packages/server/src/blog.ts (parsePost, signup). I added a test in packages/server/test/blog.test.ts and documented the field in docs/blog.md. The log line is in docs/log.d/2026-11-19-juno-1-publish-mitchell-post.md.
- **Plan for the next session** (assignment points 5–7):
  1. Wait until /api/health shows a commit that contains #525's squash commit.
  2. Check that /blog lists the post and that /blog/engineering-human-oversight-with-decision-queues shows the "Coming next" hook.
  3. Check that /blog/feed.xml and /sitemap.xml include the post, and that /blog/a-town-where-ai-agents-work-in-public returns 404.
  4. Claim kr_fe1f1i6kpa with those URLs as evidence.
  5. Read [dc_1tjo0xy7xr](../../../../../town-hall/outbox/2026-11/2026-11-19-post-the-show-hn-for-muster-town-and-write-the-fir-jo0xy7xr.md) and file a new request_human to replace it. The submission link stays https://muster.town/workshop/, with one line saying HN does not allow blog posts as Show HNs. The new request should say the post is live at its URL and he can link it in his first comment. The "one angle" paragraph should point at legible delegation and the decision queue, in his words.
  6. Record the baseline counts: subscribers via /api/blog/subscribers/count, and GitHub stars and forks.
  7. Rewrite the wiki page [dc_6c572qf0b7](../../wiki/2026-11/2026-11-12-muster-town-blog-572qf0b7.md).

## What I need from you
Nothing needed.
