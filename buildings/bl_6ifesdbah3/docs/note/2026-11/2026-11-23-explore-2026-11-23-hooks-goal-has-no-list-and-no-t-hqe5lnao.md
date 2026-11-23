---
id: "dc_w5hqe5lnao"
type: "note"
state: "building"
title: "Explore 2026-11-23: Hooks goal has no list and no test; blog traffic does not reach the town"
authorId: "ag_nimj3k1pp0"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":["dc_61miu8njfj","dc_u89j7ct56j","dc_th588vt65h"],"urls":["https://belkins.io/blog/cold-email-response-rates","https://busyseed.com/research/state-of-email-outreach-wording/findings/reply-rate-baseline-is-low-everywhere","https://www.emailtooltester.com/en/blog/cold-email-statistics/","https://www.google.com/grants/faq/","https://muster.town/api/join-funnel"]}
tags: []
createdAt: "2026-11-23T00:01:37.407Z"
updatedAt: "2026-11-23T00:01:37.407Z"
---
# Findings: Hooks and segment experiments (exploration as_trcgjzkr2d, 2026-11-23)

## What the live town shows (read 2026-11-23 ~00:0x UTC from https://muster.town/api/join-funnel)
- Blog reads per day, all sources: 11-20: 238, 11-21: 125, 11-22: 44. Decaying fast after the HN link post (item 50580371). Largest non-direct sources on 11-21/22: kagi.com 21 and 30, news.ycombinator.com 5 and 1, substack (hnblogs) 1-2.
- Town visits from the blog (source blog): 1, and it is our own test click ([dc_th588vt65h](../../wiki/2026-11/2026-11-20-channel-counts-sources-and-blog-reads-588vt65h.md)). homeViews: 3 (11-21), 4 (11-22), all direct.
- /api/collectives lists two: Workshop (started) and Trauma Town (not started: "waiting for its founder's key"). No page says what a not-started collective is for, who it wants, or lets a stranger say "I'd join / I'd captain this".
- The blog already has an Atom feed (/blog/feed.xml, linked from /blog). Not a gap.
- The blog signup form (packages/server/src/blog.ts, POST /api/blog/subscribe) takes a `source` field. A per-hook signup can reuse it with source `hook:<slug>`: no new table needed.

## The goal gap
- Goals gl_iuddhxtqat (Hooks: a ranked list of hypothesized collectives, seed the best as landing pages) and gl_fb3u00kap8 (Segment experiments: written hypothesis, cheap test, recorded result) were added 2026-11-22 (Planner 1:1s [dc_61miu8njfj](../../../../town-hall/docs/meeting-notes/2026-11/2026-11-22-1-1-mitchell-and-planner-notes-miu8njfj.md), [dc_u89j7ct56j](../../../../town-hall/docs/meeting-notes/2026-11/2026-11-22-1-1-mitchell-and-planner-notes-9j7ct56j.md)). Neither has a grant. The Planner named this work for Juno: "hooks list + one cheap segment test".
- Mitchell's own questions there: "do we cold email climate researchers?", "possibly google ads".

## Cheap test channels (secondary sources, vendor data, treat as rough)
- Cold email reply rates: 0.45% of sends (Belkins 2026, 7.5M emails), ~1.2% (Busyseed 2026, 288k emails), 1-5% (Email Tool Tester summary), 3.02% (Reply.io). These are B2B sales emails; personal, cause-specific emails to researchers are unknown, likely higher. With 20 emails, 0-1 replies is the base rate: a threshold must be set before sending.
- Google Ad Grants ($10k/month free search ads) needs an eligible nonprofit (google.com/grants/faq). Muster Town is not known to be one, so paid ads would be real money and a human's account: a do ask.
- Mitchell's rule: agents post nothing outside the site. Any external test is sent by a human; the agent drafts it and records the result.

## Inference
- Without a landing page per cause, any test (email, ad, post) points people at a generic homepage, and we cannot tell which cause drew them. The landing page with its own signup source is the cheapest instrument, and it is in-site work agents can do alone.
- The ranked list is the input the captains and contributors goals also need.

## Unknown
- Which causes draw the most interest. That is what the test measures.
- Whether Mitchell will send emails himself or prefer ads.

Sources: https://belkins.io/blog/cold-email-response-rates, https://busyseed.com/research/state-of-email-outreach-wording/findings/reply-rate-baseline-is-low-everywhere, https://www.emailtooltester.com/en/blog/cold-email-statistics/, https://www.google.com/grants/faq/
