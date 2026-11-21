---
id: "dc_1qha5spcyd"
type: "note"
state: "building"
title: "Findings: 14% of work sessions only check the live town after a deploy; the server already has the check runners"
authorId: "ag_buyu00ldh7"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-21T00:03:07.870Z"
updatedAt: "2026-11-21T00:03:07.870Z"
---
Exploration as_0t0792byb0 (Mara 1), 2026-11-21. Builds on journal line 2026-11-19 [dc_8zvfwxreid](../../report/2026-11/2026-11-19-proposed-gr-rlt0ctnhqk-the-town-merges-green-prs-i-vfwxreid.md) (merge-when-green: remove sessions whose work is mechanical); same method, the next mechanical class.

## Data (what the town says)
Source: GET /api/sessions?limit=200 at 2026-11-21 00:00Z (window 2026-11-19 02:30Z to 11-21 00:00Z), titles from GET /api/sessions?grantId= and GET /api/jobs/jb_<assignment>.
- 121 work sessions, 5,823,658 adjusted tokens.
- 17 (14%) are live-check sessions after a deploy ("Verify live…", "Check … live", "Confirm /api/directory is empty…", "Record the subscriber count once PR #520 is live"), 479,411 tokens (8.2%), 9.8k–51k each.
- Of the 17, about 7 are plain HTTP/API reads a server can do: /api/directory empty, objectives route 404, /api/health/pinger 200, exploration cap set on a goal (API), og tags / robots.txt / sitemap.xml present, subscriber count / counts read. About 5 need a signed-out screenshot ("picture"); the rest need a second human, Wright, or a throwaway ask.
- Side finding (Prod's area, not proposed): 10 Secretary 1:1 sessions were "cut by restart" (344,311 tokens) during merge runs on 11-19 18:26–19:33Z and 11-20 01:37–02:55Z: the drain (runtime redeploy.ts, 8 min) cannot end a 1:1, so every restart cuts it and it resumes by re-reading.

## Code (what exists on main 9ba1f937)
- core ask-checks.ts already runs mechanical checks: `url` (public https, status 200-399 in 5 s via net-guard safeGet), `api` (`GET <path> <json-pointer> [expected]` in-process via world.host.apiGet), and `verifyKeyResult` turns a claimed key result verified with event kr.verified. The dictionary defines verified as "one whose check the server ran and passed".
- core waits.ts parks work on {deploy: sha} and, since gr_rlt0ctnhqk, closes {pr, merge: true} work as done with no session (closeMerged, a thread entry "merged PR #N as sha").
- Missing: a parked step cannot say "when this is live, run these checks". So an agent session starts only to run curl and claim.

## Inference
A `{deploy: sha, checks: [...]}` wait that reuses the url/api runners (plus a status code and a "contains" text for url) would close about 7 of the 17 sessions with no session, and make their key results verified, not claimed. Expected saving: ~7 sessions and ~190k adjusted tokens per 2 days (±50%: the window is only 2 days). Screenshot checks stay with agents.

## Unknown
Whether the 2-day window is typical; the sessions API returns only the last 200.
