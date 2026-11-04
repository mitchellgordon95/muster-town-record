---
id: "dc_tyww89d84s"
type: "report"
state: "building"
title: "Bounties design doc: PR #182 (docs/bounties.md), note dc_2demsiwni3"
authorId: "ag_oeixoa4wjy"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_2demsiwni3","dc_bq7yfn5dr8","dc_arcy43hyut","dc_vzqoh7ppen"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/182"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. Docs-only PR #182 (878b398) plus note dc_2demsiwni3; escrow via a hosted collective with the poster's key as its one Bank input, consistent with the post-mortem rule; Ask-to-own (gr_bwm0iz7rwl) first in the build order. Mitchell reads it and answers the 5 open questions before step 2; they go in the rollup as that item's Your call. Nothing else to build now."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T20:24:27.099Z"
sessionId: "se_xgul10faqr"
assignmentId: "as_xqyll8jos5"
costUsd: 1.3959621000000002
tokens: 69798
turns: 31
createdAt: "2026-10-31T20:23:45.901Z"
updatedAt: "2026-10-31T20:24:27.099Z"
---
## What I did
I wrote docs/bounties.md, which covers Mitchell's idea from 1:1 mt_3jtclcoxl2: two home tabs and token bounties that are looking for a captain. I checked it against main 8a3a510: server home.ts and hub.ts, web home/*, core bank.ts, free-tokens.ts and goals.ts, and migration 067.
- PR: draft https://github.com/mitchellgordon95/muster-town/pull/182 (head 878b398). Docs only, no code, so there is nothing to run or deploy.
- The same text is filed as note [dc_2demsiwni3](../../note/2026-10/2026-10-31-design-bounties-home-tabs-funding-looking-for-a-ca-emsiwni3.md).
- Length: 1,482 words of prose, plus the SQL block.

## Findings
These are the main recommendations in the doc:
- **Tabs.** "Collectives looking for funding" is today's tile list, with a "N free tokens" line and a Donate link added to each tile. "Looking for a captain" shows one card per bounty: the goal, Wanted, tokens, the poster, the closing date, the number of asks, and a **Captain this** button. Both tabs are server-rendered links, so they work without JS.
- **Posting.** Anyone signed in with GitHub can post a bounty, up to 3 open each, using their own API key. This is the same rule as Start a collective.
- **Where the tokens sit.** The key is not stored in a hub table. That would break the post-mortem rule (dc_bq7yfn5dr8) that the Bank is the only place a credential lives. Instead, posting a bounty creates a hosted collective through the existing `Hub.create` path. It has no buildings and no runtime, and the poster's key is its one Bank input (`addInput`, with the bounty's tokens instead of `STARTER_KEY_TOKENS`). Nothing can spend while the bounty is open, and that is the escrow.
- **Why not `bank_reservations`.** It doesn't fit: a reservation is a per-World claim for one exploration session, and a bounty exists before any World does.
- **Expiry or withdrawal.** `Hub.retire` closes the collective and `bank.cancelInput` wipes the key (checked: it already does this).
- **Captain this.** It is the Ask-to-own request of gr_bwm0iz7rwl, made on the bounty collective's root goal. The poster accepts it from that collective's Town Hall in-tray and deck. On accept, the captain becomes admin and owner of the root goal, the hub row's owner changes to the captain, and the runtime starts. I chose this over attaching the bounty to an existing collective, which would put a stranger's key in another collective's Bank.
- **Data model.** One new `bounties` table in hub.db, made with CREATE TABLE IF NOT EXISTS. hub.db has no migration runner, so no World migration is needed. The doc lists the routes under `/api/bounties`.
- **Build order, six PRs.** Ask to own (gr_bwm0iz7rwl) comes first. Step 3 (posting a bounty) touches the Bank, so Mitchell has to approve it first.
- **Open questions for Mitchell (5).** Who posts; whether the Workshop's own Bank can fund bounties (its subscription token can't fund another collective under today's terms); the poster's role after accept; the caps; free-text Wanted vs tags.

## What I need from you
Mitchell: answer the 5 open questions in docs/bounties.md §6 (PR #182) before step 2 is built.
