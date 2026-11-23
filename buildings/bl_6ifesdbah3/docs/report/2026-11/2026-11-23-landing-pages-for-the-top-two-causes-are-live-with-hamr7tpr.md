---
id: "dc_rihamr7tpr"
type: "report"
state: "building"
title: "Landing pages for the top two causes are live with their own signups and view counts"
authorId: "ag_7fwioi3hez"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: the next step is queued."
decidedBy: "system"
decidedAt: "2026-11-23T16:58:13.506Z"
sessionId: "se_dzwb43o0ad"
assignmentId: "as_5b9c9pn17e"
costUsd: 2.0227235
tokens: 101136
turns: 41
createdAt: "2026-11-23T16:58:13.416Z"
updatedAt: "2026-11-23T16:58:13.506Z"
---
## What I did
I built PR #576 (https://github.com/mitchellgordon95/muster-town/pull/576). CI passed, I merged it as e3fd8992, and it went live at 86f24796 (/api/health startedAt 2026-11-23 16:57:02Z). It serves `/hooks/<slug>` from published Outreach notes tagged `hook`, so adding a new cause's page needs a doc, not a PR. Each page ends with a signup sent as `hook:<slug>`. I widened the mailing-list SOURCE regex so it accepts that form, and the confirmation email now names the cause's page instead of the blog. Each page's views count per slug in a new `hookViews` array in /api/join-funnel. `/hooks` lists every landing page above the ranked list. I added tests in blog, mailing-list and join-funnel: 34 pass, and typecheck is clean. I documented it in docs/blog.md. Then I published the two pages: [C-PTSD research collective](../../note/2026-11/2026-11-23-a-research-collective-for-complex-ptsd-and-dissoci-it4kgvky.md) at /hooks/cptsd and [Climate adaptation data collective](../../note/2026-11/2026-11-23-a-climate-adaptation-data-collective-for-one-regio-xbmqlwni.md) at /hooks/climate-adaptation.

## Findings
- **Checked on the live site at 16:57Z.** Both pages return 200 and carry `data-source="hook:cptsd"` and `"hook:climate-adaptation"`. /hooks links both. One browser-UA view of each page (`?ref=check`) shows in /api/join-funnel `hookViews`, one row per slug. Each page got one test signup to `delivered+hook-<slug>@resend.dev`; each answered `{ok:true, confirm:true}`. The subscriber count is now 6, with 3 confirmed; it was 4 on 11-20.
- **Not checked by me:** the `hook:<slug>` source in the subscriber export. GET /api/blog/subscribers refuses agent tokens ("needs a user token"). The stored source is covered by a unit test only. Mitchell can see both test rows in the export.
- I recorded the baseline and the test rows to subtract (2 views, 2 signups, all ours) on [Channel counts](../../wiki/2026-11/2026-11-20-channel-counts-sources-and-blog-reads-588vt65h.md). The Hooks topic page [dc_5rr8n7dqf8](../../wiki/2026-11/2026-11-23-hooks-ranked-causes-r8n7dqf8.md) now says how to add a page.
- I merged it myself, inside this session, so I could verify it live before reporting. I did not park it with merge-when-green.

## What I need from you
Nothing needed.
