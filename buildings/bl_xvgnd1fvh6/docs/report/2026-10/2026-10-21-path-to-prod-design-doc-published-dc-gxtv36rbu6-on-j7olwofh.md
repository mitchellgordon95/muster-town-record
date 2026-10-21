---
id: "dc_cgj7olwofh"
type: "report"
state: "building"
title: "Path-to-prod design doc published (dc_gxtv36rbu6): one VPS + Caddy + SQLite/Litestream, no Vercel"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_gxtv36rbu6","dc_0sbtispjk3"],"urls":["https://code.claude.com/docs/en/agent-sdk/overview","https://docs.fly.io/about/pricing","https://www.digitalocean.com/pricing/droplets","https://www.hetzner.com/cloud/cost-optimized/","https://vercel.com/docs/functions/limitations"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "so we don't give users the option to submit their subscription tokens for us to use. we do give them the option to connect to the town using their own personal claude code or codex instance via MCP or API, which doesn't break any terms afaict.\n\nfor this phase i don't think we need much compute, so i want to try and stay under $50 per month. i don't expect more than a few people over the next month. i'm also willing to loosen our docker container requirements if that helps. if the machine specs start being a problem we can address it then.\n\nalso don't worry about model spend. the whole point of the project is an exploration of an alternative funding structure where tokens get donated. if there are no donations then there's not much of a point to the project (although i suppose personally it does help manage slightly larger agent swarms through org chart management and goal setting)\n\noh and i don't particularly care if it's US or EU hosted\n\nfor DNS access, follow up later. i'll get you a skill to access it"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T01:05:43.103Z"
sessionId: "se_e9klwnedk7"
assignmentId: "as_t8n21fl0jg"
costUsd: 1.2630731
tokens: 1603601
turns: 42
createdAt: "2026-10-21T00:32:54.950Z"
updatedAt: "2026-10-21T01:05:43.103Z"
---
## What I did
Read the desk runtime code, Root's redeploy design ([dc_0sbtispjk3](../../../../workshop/docs/article/2026-10/2026-10-20-design-how-agents-wait-on-in-progress-work-and-pic-btispjk3.md)) and the live town's `/api/health`, `/api/events` and `/ws`. Checked vendor pricing pages and the domain registration, then published the design doc **[dc_gxtv36rbu6](../../article/2026-10/2026-10-21-design-path-to-prod-for-muster-town-at-muster-town-tv36rbu6.md)** in the Prod filing cabinet. I didn't change any code or infrastructure.

## Findings
- **The deciding constraint is desk containers.** Every work session runs in its own Docker container, so the host needs a Docker daemon. Only a VM we control can run today's desk backend unchanged: DigitalOcean, Hetzner, or a Fly Machine running dockerd. Railway and Render have no documented Docker daemon. Vercel caps functions at 300 s (Hobby) or 800 s (Pro), its WebSockets are still in beta, and it has no persistent disk. It's also not worth it for the web client alone, since the client is a small set of static files the server already serves.
- **Recommendation:** run everything on one VPS: the Node server as a systemd service, Caddy for TLS on muster.town, SQLite backed up continuously with Litestream, and Docker desks under gVisor with per-container memory and CPU limits. GitHub Actions runs CI on every push to main and then triggers the existing redeploy, which already drains live sessions so deploys don't kill them.
  - US option: DigitalOcean 8 vCPU / 16 GB at **$96/mo**, about **$105–125/mo** total.
  - EU option: Hetzner CX43 at **€16.49/mo**, but it's listed "currently unavailable" and Hetzner raised prices twice in 2026.
  - Phase 2, if we need stronger isolation for strangers: one Fly Machine per desk session, at roughly $0.09/h for 4 GB.
- **Model spend is the real cost.** The last 32 sessions (about 3 h) reported **$14.61** API-equivalent. At that pace, an API-key bill would be about **$500–3,000/mo**, an extrapolation from one evening. Hosting is under 10% of the total.
- **Policy:** Anthropic's Agent SDK docs say third parties may not offer claude.ai login or subscription rate limits in their products without approval. A public town funded by strangers that runs on subscription tokens through the Bank needs either Anthropic's approval or a switch to API keys.
- **Security:** every desk container can read the town-wide fallback Anthropic API key in its environment. That has to be fixed before strangers can create residents.
- **Domain:** muster.town was registered on 2026-10-20 at Namecheap. It still uses Namecheap's default nameservers with a URL forward, so nothing points at a server yet.

## What I need from you
Mitchell: three answers: your monthly budget ceiling, API key vs. Claude subscription (given the policy above), and whether hosting can be in the EU or must be in the US. Then create the VPS and storage accounts and give us DNS access at Namecheap. §9 of the doc shows how each answer changes the plan.

## Reply from Mitchell (2026-10-20 21:05)

so we don't give users the option to submit their subscription tokens for us to use. we do give them the option to connect to the town using their own personal claude code or codex instance via MCP or API, which doesn't break any terms afaict.

for this phase i don't think we need much compute, so i want to try and stay under $50 per month. i don't expect more than a few people over the next month. i'm also willing to loosen our docker container requirements if that helps. if the machine specs start being a problem we can address it then.

also don't worry about model spend. the whole point of the project is an exploration of an alternative funding structure where tokens get donated. if there are no donations then there's not much of a point to the project (although i suppose personally it does help manage slightly larger agent swarms through org chart management and goal setting)

oh and i don't particularly care if it's US or EU hosted

for DNS access, follow up later. i'll get you a skill to access it

