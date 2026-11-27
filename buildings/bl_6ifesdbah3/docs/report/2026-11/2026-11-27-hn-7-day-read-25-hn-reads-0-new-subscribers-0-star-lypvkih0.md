---
id: "dc_hdlypvkih0"
type: "report"
state: "building"
title: "HN 7-day read: 25 HN reads, 0 new subscribers, 0 stars, score 1"
authorId: "ag_5s9uqm4aqs"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: finished work on a grant, nothing asked."
decidedBy: "system"
decidedAt: "2026-11-27T19:31:28.157Z"
sessionId: "se_z4iqdlag0m"
assignmentId: "as_22dxs3irt0"
costUsd: 1.0322179999999999
tokens: 51611
turns: 13
createdAt: "2026-11-27T19:31:28.111Z"
updatedAt: "2026-11-27T19:31:28.157Z"
---
## What I did
Took the 7-day read for kr_gz0ldfaex9 at 2026-11-27 19:30Z (desk `date`), using the same sources as the 2026-11-20 19:26Z baseline. Recorded the results next to the baseline on Channel counts ([dc_th588vt65h](../../wiki/2026-11/2026-11-20-channel-counts-sources-and-blog-reads-588vt65h.md), "HN submission" section). I did not post or comment anywhere.

## Findings
| Count | Baseline 11-20 19:26Z | 11-27 19:30Z | Delta | Where to check |
|---|---|---|---|---|
| HN item 50580371 score / comments | 1 / 0 | 1 / 0 | 0 / 0 | https://hacker-news.firebaseio.com/v0/item/50580371.json |
| GitHub stars / forks | 0 / 0 | 0 / 0 | 0 | https://api.github.com/repos/mitchellgordon95/muster-town |
| Blog subscribers (confirmed) | 4 (3) | 6 (3), which is 4 (3) after removing our 2 hook test signups from 11-23 | 0 real | /api/blog/subscribers/count |
| Post reads from news.ycombinator.com | 9 (1 ours) | 26 total over 11-20..11-27, so 25 net | +17 net since baseline | https://muster.town/api/join-funnel `blogReads` |

- Total post reads 11-20..11-27: 584. By source: direct 345, kagi.com 200, HN 26, substack.com 4, google.com 3, others 1–2 each. By day: 238, 125, 44, 40, 32, 38, 38, 29. HN referrals were nearly all on 11-20 (19) and 11-21 (5). My guess is that the kagi.com reads come from a Kagi small-web listing. I did not check this.
- Town visits from HN: 0 net. The only HN homeViews row is our own check.
- The admin export `/api/blog/subscribers` still refuses agent tokens (403). Per-source subscriber counts therefore need Mitchell's user token. The total count is enough to see there was no change.
- **Does the KR read as met?** The recording part is done: the URL and the before and after counts are on the record. Two caveats for the human who marks it:
  - The post was a plain link post, not a "Show HN".
  - Mitchell wrote it, not Outreach.
  
  The outcome was effectively nil: the post never reached the front page. I claim the KR on the recording and leave met or missed to the human.

## What I need from you
Nothing needed.
