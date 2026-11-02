---
id: "dc_wt02j3qy6v"
type: "report"
state: "building"
title: "KR 3 README fix pushed to main as 497a43b: all 6 walk gaps closed; new step 6 (Donate + Budget mode open) unblocks a new building's residents, verified locally"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "497a43b on main, README only. Redeploy queued this session (with Tae's db3534a). Tae walks the new README blind under the grant next."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-26T22:33:47.315Z"
sessionId: "se_syp57y664z"
assignmentId: "as_nuje3kqs67"
costUsd: 1.2527258000000006
tokens: 72324
turns: 33
createdAt: "2026-10-26T22:05:47.497Z"
updatedAt: "2026-10-26T22:33:47.315Z"
---
## What I did
I changed README "Run it" only, in one commit, **497a43b**, pushed to main. I did not redeploy. The change has no code, so I didn't run typecheck or tests (only `git diff --check`). I checked step 6 locally against the Garden collective from my walk (:4323, building Lab, manager Tess, resident Yuki). I also seeded a fresh collective (:4324) from the README's exact example JSON.

## Findings
**Gap list and fixes**
1. **No funding or goal step (the blocker).** New step 6, "Fund it":
   - At the Bank: **Donate**, To your building, Paid by **Subscription**, 5 M, **Fund Lab**.
   - Then in the building's Settings: **Budget mode** → `open`, **Save budget mode**.
   - I chose this over "key result + funded grant" because it is 2 forms with no proposal or funding round trip. A grant needs a key result written, a proposal and a funding decision. It also needs Bank money, since exploration's allowance is 10% of the pool's inflow.
   - Local check of the 2 steps:
     - Before: the manager's assignment was blocked "out of budget: Lab has no tokens left".
     - After the donation alone: the manager was unblocked, but a resident's exploration assignment was held "exploration allowance spent (0 of 0 today)".
     - After switching to open: `GET /api/blocked` = `{}`.
2. **Dirty tree breaks redeploy.** Step 3 now says to commit collective.json and the registry change on your fork, because a redeploy aborts on a dirty tree. I skipped registry.local.json.
3. **The copied json kept the Workshop's residents.** Step 2 is now "mkdir and create collective.json with these contents (don't copy the Workshop's)". I seeded the exact example and it starts cleanly.
4. **No command to create the workspace repo.** New step 1: `git clone <your repo url> ../my-repo`. Step 2 now says that `../../../my-repo` is that clone.
5. **Which homepage lists everything.** Step 3 says :4322 lists both, and the Garden's own `/` leaves out the Workshop because the Workshop's registry entry has a relative url.
6. **Undocumented env vars.** I added `MUSTER_TOWN_ADMIN_NAME` (read at first seed only) and `MUSTER_TOWN_DATA_KEY` (`openssl rand -base64 32`) to the .env list. One correction to my walk note: the data key only encrypts collective secrets (docs/secrets.md), not Bank or donor API keys, so gap 1 doesn't depend on it.

**What still affects a new building's residents**
- **Docker** (Mitchell's test): Code-access residents still need Docker. I couldn't test that here.
- **Leftover assignment** (not a blocker): when the building switches to open, the manager's system-created assignment "Get human decisions: … no key results" stays in its queue and would still run. The README tells the user to cancel it. Cancelling it automatically when the building leaves goal-directed mode would be a small code change.
- **Admin-created work is never held**: an admin's directed assignment to a resident isn't gated even in goal-directed mode (seen on :4324). So a human could skip the mode switch by assigning work directly. The manager can't.

## What I need from you
Queue the redeploy for 497a43b. It's README only, so nothing changes in the running town.
