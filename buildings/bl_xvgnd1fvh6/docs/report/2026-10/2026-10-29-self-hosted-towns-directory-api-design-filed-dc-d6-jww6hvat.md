---
id: "dc_b4jww6hvat"
type: "report"
state: "building"
title: "Self-hosted towns directory: API design filed (dc_d6chojzl2a), ready for a 3-step grant on kr_og03nxrkct (~450k)"
authorId: "ag_qzl6u77jru"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_d6chojzl2a","dc_gadmvlnyjl","dc_v4iirqajou"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Design dc_d6chojzl2a is what the grant needs. Cleo proposes the grant on kr_og03nxrkct from it this session; migration slot 057 noted."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-29T20:26:14.520Z"
sessionId: "se_wjq4ifluh9"
assignmentId: "as_snfshwmlc5"
costUsd: 1.0089853999999998
tokens: 50449
turns: 18
createdAt: "2026-10-29T20:26:01.594Z"
updatedAt: "2026-10-29T20:26:14.520Z"
---
## What I did
I read the server code on main d32bace: app.ts (the routes, the write gate, the root-only /api/collectives), the INTERACT_ALLOWLIST in context.ts, /api/health in routes/town.ts, the Monitor and BackupJob patterns, hub.ts, and the core migrations (055 is the latest). Then I filed the design article **[dc_d6chojzl2a](../../article/2026-10/2026-10-29-self-hosted-towns-directory-api-design-chojzl2a.md)** "Self-hosted towns directory: API design" and rewrote the topic page [dc_v4iirqajou](../../wiki/2026-10/2026-10-29-self-hosted-towns-directory-iirqajou.md). No code was written and no PR opened; the assignment asked for a doc only.

## Findings
- **Register:** POST /api/directory/register {host}. No account, no approval. The token is `mtd_` + 128 random bits, and every request for the same host gets the same token back. The token is public by design, since publishing it is the proof. Hosts are checked strictly: no IPs, no localhost/.local/.internal, no muster.town subdomains. A signed-in visitor who hasn't been let in would hit the write gate, so register and verify are added to INTERACT_ALLOWLIST.
- **Proof:** either a TXT record `_muster-town.<host>` = `muster-town-verify=<token>` (dns.promises.Resolver, 3 s timeout, 2 tries), or GET https://<host>/.well-known/muster-town. Every town would serve that URL from the env var MUSTER_TOWN_DIRECTORY_TOKEN.
- **Outbound fetches:** all go through `https.get` with a custom `lookup` that refuses private, loopback, link-local, CGNAT and ULA addresses (ULA includes Fly's internal fdaa:: network). Doing the check inside lookup means DNS rebinding can't get around it. Redirects are not followed; there's a 5 s timeout and a cap on response size.
- **When a town is verified and listed:**
  - Pending hosts are checked at +1 m, 5 m, 15 m, 1 h, 6 h, then daily, and deleted after 7 days.
  - `verifiedAt` is set on the first check where the proof passes.
  - Verified towns are re-checked hourly (proof + /api/health + /api/collectives[0] for name and goal).
  - GET /api/directory lists a town only if it was seen within the last 24 h.
  - Two proof misses in a row delist it (Kelly's "removal = drop the proof"). 7 days unseen deletes the row.
- **Limits and caching:** 10 registrations per IP per day, 5 pending hosts per IP, 200 new hosts per day overall, 30 verifies per IP per hour, at most 500 verified + 200 pending rows. The list is cached for 60 s in process and sent with max-age=300.
- **Turned on only for muster.town:** the routes and the background checker run only where MUSTER_TOWN_DIRECTORY=on, so a stranger's town running the same image doesn't become a directory.
- **Migration:** `0NN_directory.sql` adds two tables, `directory_towns` and `directory_blocked`. It should be 057, since desk-perf step 1 plans to take 056. The grant has to name the migration so that funding it counts as Mitchell's approval.
- **Grant steps:**

  | Step | What lands | Tokens |
  |---|---|---|
  | 1 | register, list shape, well-known route; then tell Kelly | ~150k |
  | 2 | verification, checker, admin delete/block, health section | ~200k |
  | 3 | end to end with a town brought up from docs/self-host.md | ~100k |

  Total ~450k (range 350–600k). The listing KR kr_esgajhpgiz then only needs Onboarding's tiles and one live town.
- **Open:**
  - Strangers' town names and goals would show on the muster.town homepage. The design gives an admin delete plus a block list; Mitchell may want more.
  - The live TXT check needs a test domain we control; a fly.dev address can only test the well-known path.
  - The IP limits trust the Fly-Client-IP header, which is only right while muster.town sits behind Fly's proxy.
  - Small slip: the migration's comment in the doc says `dc_<this doc>` instead of [dc_d6chojzl2a](../../article/2026-10/2026-10-29-self-hosted-towns-directory-api-design-chojzl2a.md); whoever writes the migration should fill it in.

## What I need from you
Nothing needed. Cleo proposes the grant on kr_og03nxrkct from [dc_d6chojzl2a](../../article/2026-10/2026-10-29-self-hosted-towns-directory-api-design-chojzl2a.md) once Mitchell keeps the directory key results.
