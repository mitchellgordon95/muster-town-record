---
id: "dc_k3lclh314d"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-05T23:23:36.559Z"
updatedAt: "2026-11-05T23:23:36.559Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Town:** Pix is in a team-lead session; it answers between steps.
- **Pix:** Hi Mitchell. I'm mid in-tray: the throwaway grant gr_gxhmlxk1hv just ran both steps by itself (step 1 after funding, step 2 queued 7 ms after step 1's report, no manager session). What do you need?
- **Mitchell:** so we're good on all the work we were discussing earlier?
- **Pix:** Mostly, yes. A (stable fork prompt): work done, closes in my next rollup; one KR (first-turn write under 8k) misses as framed, so that rollup asks you to flip it. B (steps in the proposal, no kickoff): steps 1-2 live, and your throwaway grant just proved the last two KRs live (step 1 queued at funding, step 2 queued 7 ms after step 1's report, no manager session); I'm queueing one fork to pin the timestamps, then I close B and the throwaway. C (no checkpoint session, fork-filed KR evidence, reserve): PR #381 still parked on CI, step 2 queued behind it. D (Town health tab, gr_8bxoy2heif, 150k): proposed, waiting on you. Next rollup around 01:00Z, about 2 h from now, unless you want it sooner.
- **Mitchell:** how long until C is live?
- **Pix:** Can't see CI from here, so an estimate: C's step 1 (PR #381, head 239b8f1, a docs/deadcode fix pushed about 20 min ago) merges by itself when its checks go green (Pix 1 is parked on them), then CI on main deploys it: if it's green now, step 1 is live within about 30-45 min. Step 2 (forks file KR evidence via submit_report, held-grant card) is one fork session queued behind that merge, plus its own PR, CI and deploy: roughly another 1.5-2 h. So all of C live tonight, about 2-3 h from now, if nothing fails CI. Step 3 is then a live check that waits for the first real holds (up to 5 days), not code.
- **Mitchell:** why does it take so long to deploy?
- **Pix:** Three serial waits per PR, each a few minutes to a quarter hour. (1) CI runs the full check on the PR (npm ci, docs + deadcode checks, typecheck, tests, web build; ci.yml:24-47), then after the merge it runs the same check again on main before promote may touch prod (promote needs check, ci.yml:49-51). (2) Promote only restarts the server if it started more than 15 min ago, else it sleeps the remainder (ci.yml:69-93), the rule from the 11-04 merge storm. (3) The restart itself: pull, build, restart, drain (the comment at ci.yml:64 allows up to 30 min). C step 1 just merged (4ab6187, Pix 2 report [dc_5tbwe9c3so](../../report/2026-11/2026-11-05-grant-c-step-1-merged-pr-381-4ab6187-no-checkpoint-bwe9c3so.md)); C step 2 is a second PR, so it pays all three again. The obvious cuts: skip the main re-check for a commit already green on its PR, and let promote restart at once when nothing restarted in the last 15 min. Prod's building owns ci.yml; say the word and I'll ask Cleo for it.
- **Mitchell:** isn't "let promote restart at once when nothing restarted in the last 15 min" just rephrasing how things already work?
- **Pix:** Yes, you're right, I misread it. ci.yml:87-93 waits only for the remainder of 15 min since the server's startedAt, so if nothing restarted in the last 15 min it restarts at once. Scratch that one. The debounce only bites when merges stack up: any building's merge (or a no-op redeploy) resets the clock, so the next one waits up to 15 min; with 7 buildings merging that is often. The real fixed costs per PR are the check run twice (once on the PR, once on main before promote: ci.yml:49-51) and the restart/drain itself. Skipping the main re-check when the merge commit's tree equals a green PR head is the one real cut; everything else is the restart.
- **Mitchell:** don't tell cleo any specific fixes, but ask them to analyze the CI and (if we don't have observability there) add CI metrics so we can see what's happening. that can be a grant, and then the follow-up proposed speed-ups would be another grant
- **Pix:** Done: told Cleo, quoting you, no fixes named. Grant 1 = analyse the CI → deploy path and add CI metrics if there's no observability there; grant 2 = the speed-ups, proposed from what the metrics show. Both are Prod's to propose (ci.yml is theirs); you'll see the first in the Town Hall in-tray when Cleo files it.
- **Pix:** One more thing: Cleo was idle, and a message alone starts no work, so I also recorded it as a decision here: it's now as_hydyuiyu1v on Prod's queue (directed, from this 1:1), so a fork of Cleo picks it up and files the proposal.

## Decisions

1. Prod (Cleo): propose a grant that analyses the CI → deploy path (PR check, main re-check, promote, debounce, restart/drain) and, if there is no observability there, adds CI metrics so a human can see where the minutes go between a merge and the commit being live. No specific fixes named up front (Mitchell: "don't tell cleo any specific fixes"). The speed-ups come later as a separate follow-up grant, proposed from what the metrics show. → Prod queue (a fork of Cleo)

