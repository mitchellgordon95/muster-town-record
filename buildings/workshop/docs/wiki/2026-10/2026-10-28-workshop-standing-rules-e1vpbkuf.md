---
id: "dc_w6e1vpbkuf"
type: "wiki"
state: "building"
title: "Workshop standing rules"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "workshop"
createdAt: "2026-10-28T02:03:59.985Z"
updatedAt: "2026-11-16T18:13:14.641Z"
---
State on 2026-11-16 (Pix 3, as_5byord3vip, from 1:1 mt_dm14dgejml). The Town Workshop's standing rules, as a building-owned topic page (loaded by forks).
- **No pause in force.** Mitchell lifted the 11-12 pause (mt_og21m12bcs, "pause your work until the job refactor is done") on 2026-11-16 at 18:11Z: "ok yeah i think we're unblocked" (mt_dm14dgejml decision 10). Grant, directed and retainer work run; the rule "no queue, jobs or report-rule code" is over. The job refactor is done: build on topic page [dc_skk467jd88](../2026-11/2026-11-12-jobs-and-entries-gr-9mp6v6vv8k-k467jd88.md), not on the plan.
- **Decisions are made in the Town Hall queue, not in chat** (mt_dm14dgejml decision 1; docs/engineering-human-oversight.txt). What only a human can settle is one need, rendered as one card with `ask`. A meeting is for items that need discussion before they become a card.
- **No rollups.** They are retired (01253807). What shipped goes in `close_grant` `shipped`; what a human must settle goes through `ask`; the rest is the record on the job threads.
- **Work routing:** work naming a forking manager or a fork lands on the building queue (core domain.ts createAssignment). What a manager must decide (a tell, a mention, a grant countered, rejected or cut, a dead session) is an entry on a job's thread, decided with `review` on its en_ id.
- Early stage: a manager or fork merges its own green PR to main without asking. Run typecheck and the test files your change touches before pushing; main CI is the authority for the full suites.
- Tests on a desk: 2 CPUs, little RAM. Run single test files in the foreground with a timeout (`timeout 90 npx vitest run <file> --reporter=dot`), never the whole suite, and never wait on a background task.
- Ask Mitchell first only for Bank or token-accounting changes, or anything touching another building's code (town-wide [dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-11-05-ci-deploy-qoh7ppen.md)).
- Schema migrations ship with the PR: additive and backward compatible. Migration numbers must be unique; check the highest on main right before merging (116 on 11-16).
- **CI deploys your merge; never call `redeploy`** ([dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-11-05-ci-deploy-qoh7ppen.md), [dc_uzwcg5xw3u](../../../../town-hall/docs/fyi/2026-11/2026-11-04-do-not-call-redeploy-after-a-merge-ci-deploys-gree-wcg5xw3u.md)). Say which commit should be live and park the live check; `GET /api/health` commit + `git merge-base --is-ancestor` tells when it is live.
- Town log entries go in docs/log.d/<date>-<branch-slug>.md, never docs/log.md ([dc_0g5zclwr09](../../../../town-hall/docs/fyi/2026-11/2026-11-10-town-log-entries-now-go-in-docs-log-d-not-docs-log-5zclwr09.md)).
- Never cut text a human might need to read: wrap it or use ShowMore (web ui.tsx); no bare slice + "…" (mt_rt8rbn4ban).
