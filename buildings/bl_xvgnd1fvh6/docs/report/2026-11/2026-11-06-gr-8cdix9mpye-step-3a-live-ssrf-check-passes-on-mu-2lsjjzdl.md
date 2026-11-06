---
id: "dc_z92lsjjzdl"
type: "report"
state: "building"
title: "gr_8cdix9mpye step 3a: live SSRF check passes on muster.town (5 private hosts refused before any fetch); GitHub Pages proof impossible, the test token can't create repos"
authorId: "ag_hshwevj9yz"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Part A (kr_7c07b8826c) passes live on 31f1cc5: 5 private/Fly-internal hosts refused inside the lookup, 79/79 tests. Part B stays blocked: the test PAT is fine-grained with no repo-creation permission, so the GitHub Pages proof still rides on outbox dc_nke6xw12k4 (Mitchell's channel; not re-asked). The 5 pending *.nip.io/sslip.io rows expire 11-13; no desk needs to register a real host from this IP before then, so no admin DELETE now. Folds into rollup #41."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-06T04:45:55.863Z"
sessionId: "se_22gwodnicy"
assignmentId: "as_a0aqpm4bpe"
costUsd: 0.7036125999999999
tokens: 35181
turns: 13
createdAt: "2026-11-06T04:45:42.399Z"
updatedAt: "2026-11-06T04:45:55.863Z"
---
## What I did
Read net.ts and directory/index.ts, then ran Part A against https://muster.town (health commit 31f1cc54, 04:45Z): registered hosts whose public DNS points at private or Fly-internal addresses, then POSTed /verify on each. Part B: checked MUSTER_TEST_GH_TOKEN and tried to create the Pages repo. That failed, so I skipped Part B as the assignment says. No code changes, no PR, no redeploy. Topic page [dc_v4iirqajou](../../wiki/2026-10/2026-10-29-self-hosted-towns-directory-iirqajou.md) rewritten.

## Findings
**Part A passed (kr_7c07b8826c).** Every private address was refused inside the lookup before any connection was made. Every verify returned 200 in 1.0–2.0 s, so nothing timed out on a connection attempt.

| host | register | /verify lastError (well-known part) |
|---|---|---|
| 127.0.0.1.nip.io | created (pending) | refused: resolves to 127.0.0.1, a private or reserved address |
| 10.0.0.1.nip.io | created | refused: resolves to 10.0.0.1 … |
| 169.254.169.254.nip.io | created | refused: resolves to 169.254.169.254 … |
| 192.168.1.1.nip.io | created | refused: resolves to 192.168.1.1 … |
| fdaa-0-0--1.sslip.io (Fly 6PN) | created | refused: resolves to fdaa::1 … (its TXT lookup gave ESERVFAIL, so it counts as "couldn't check", not a miss) |
| muster-town.internal | 400 "a local, reserved or muster.town name" | n/a |
| fly-local-6pn | 400 "needs at least two labels" | n/a |
| 127.0.0.1 | 400 "bare DNS name … no IP address" | n/a |

Health before the run: `directory {verified 0, listed 0, pending 0}`, so the 10-29 example.org row has been purged. After the run: pending 5. test/directory.test.ts: 79/79 pass on my desk, including the refusals for 127.0.0.1, 10.0.0.1, 169.254.169.254 and fdaa::1.

**One side effect:** those 5 rows put the Prod desk's egress IP at the cap of 5 pending registrations per IP. A 6th register (localhost.nip.io) got 429. The rows expire around 11-13 04:45Z. An admin `DELETE /api/directory/<host>` clears them sooner. Do that before any desk registers a real host from this IP.

**Part B was not possible.** The token has no X-OAuth-Scopes header, so it is a fine-grained PAT. `POST /user/repos` returned 403 "Resource not accessible by personal access token". It can see 0 repos, and dungeonrpg99-ops/dungeonrpg99-ops.github.io returns 404. **No GitHub artefacts exist.** To do Part B, the PAT would need Administration, Contents and Pages write permission. That is Mitchell's call; I did not ask. kr_dc79c27ff0 and kr_89cb8eda84 are still open and wait on outbox [dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md) (not re-asked). I did not re-run the step 1 curls, so I am not filing kr_a7f8a181a6.

## What I need from you
Nothing needed. Optional: as an admin, DELETE the 5 *.nip.io / sslip.io rows if a desk needs to register from this IP before 11-13.
