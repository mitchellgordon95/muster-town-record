---
id: "dc_1gostt95ta"
type: "report"
state: "building"
title: "Blog email signup is live; the only thing left to check is Mitchell's own read of the subscriber list"
authorId: "ag_rdbd5rmxg3"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Email signup verified live at 0a682c67. Admin read of the list goes to Mitchell in rollup #4 as a one-click check."
decidedBy: "ag_qtxi6eg1ul"
decidedAt: "2026-11-12T16:22:57.852Z"
sessionId: "se_xh3191n5zp"
assignmentId: "as_9lkb0f3tit"
costUsd: 0.4060194000000001
tokens: 20301
turns: 11
createdAt: "2026-11-12T16:22:44.544Z"
updatedAt: "2026-11-12T16:22:57.852Z"
---
## What I did
At 16:22 UTC the live server was on 0a682c67, the PR #433 merge (https://github.com/mitchellgordon95/agent-town/pull/433). I checked the form on the live pages, subscribed a test address and tried the admin export with every token I have. I updated the topic page [dc_6c572qf0b7](../../wiki/2026-11/2026-11-12-muster-town-blog-572qf0b7.md).

## Findings
- **The form is live.** It sits at the foot of https://muster.town/blog/hello-from-muster-town and of https://muster.town/blog. It has one input, a "Sign up" button, the line "New posts by email. Nothing else." and a hidden honeypot field.
- **Subscribing works.**
  - `POST /api/blog/subscribe` with juno-verify-1794500532@example.com (sent upper-cased, source hello-from-muster-town) answered 200 `{ok:true}`.
  - Sending the same address again also answered 200.
  - `"not an email"` answered 400 with "That doesn't look like an email address."
  - That test address is now in the list. Mitchell can ignore it or delete it.
- **The export turns away everyone but admins:**
  - no token gets 401
  - my agent tokens get 403 "This endpoint needs a user token"
  - the non-admin test user dungeonrpg99-ops gets 403 "Only an admin of this town can read the mailing list", for both JSON and `?format=csv`
- **Not checked live: an admin actually reading the list, or the subscriber count.** No agent has an admin user token. The admin path passed in PR #433's tests. The server also accepts the browser session cookie, so Mitchell can check it in one click while signed in: https://muster.town/api/blog/subscribers?format=csv. He should see at least the one test row.
- No confirmation email and no unsubscribe link, because the town has no mail sender. This was already said in rollup #3.

## What I need from you
Nothing needed. For rollup #4: ask Mitchell to open https://muster.town/api/blog/subscribers?format=csv while signed in to confirm the admin export.
