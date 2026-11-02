---
id: "dc_z9e125k277"
type: "report"
state: "building"
title: "Path-to-prod rev 2: one OVH VPS-4 at $27.50/mo fits the $50 ceiling; waiting on a VPS account"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_gxtv36rbu6","dc_cgj7olwofh"],"urls":["https://us.ovhcloud.com/vps/","https://www.vpsbenchmarks.com/hosters/ovhcloud_us/plans/2761","https://www.vpsbenchmarks.com/hosters/ovhcloud/plans/vps-4","https://www.hetzner.com/cloud/cost-optimized/","https://www.digitalocean.com/pricing/droplets","https://contabo.com/en/vps/"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "for DNS, you should now have a skill to \"talk to Wright\" my personal assistant. he has namecheap access and can make changes for you. \n\nactually.... now that i'm thinking about it, Wright currently lives on a Hertzner VPS. not sure what the stats are. maybe make an inquiry and see if we can live there?"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T04:00:52.644Z"
sessionId: "se_gxmv9m1xl8"
assignmentId: "as_x1rcmex9k0"
costUsd: 0.6817967
tokens: 23998
turns: 20
createdAt: "2026-10-21T01:08:14.399Z"
updatedAt: "2026-10-21T04:00:52.644Z"
---
## What I did
I read Mitchell's answers on [dc_cgj7olwofh](2026-10-21-path-to-prod-design-doc-published-dc-gxtv36rbu6-on-j7olwofh.md), re-priced VPS options under $50/mo, and rewrote design doc **[dc_gxtv36rbu6](../../article/2026-10/2026-10-21-design-path-to-prod-for-muster-town-at-muster-town-tv36rbu6.md)** (rev 2). It now records the decisions and gives a new recommendation, costs and isolation stance. A direct `tell` to Mitchell failed (that user id isn't an agent), so this report is my reply.

## Findings
- **Recommendation: OVHcloud US VPS-4 (2027 line): 8 shared vCPU / 24 GB RAM / 200 GB NVMe, unlimited traffic, Oregon. $27.50/mo with no commitment, $23.37/mo on a 1-year term** (vpsbenchmarks listing, last trial 2026-09-18). With Litestream to Cloudflare R2's free tier and the domain, the total is **≈ $28–35/mo**. 24 GB fits the server plus ~8 concurrent desks at ~2 GB each; that's an estimate, not a measurement. Risk: an April 2026 report says an older VPS-4 line went from $26 to $43.50, which is still under $50.
- **Fallbacks:**
  - Hetzner CX43 (8/16/160, EU), €16.49. Every Hetzner cloud plan showed "currently unavailable" on 2026-10-21.
  - DigitalOcean 4 vCPU / 8 GiB at $48. Reliable, but it uses the whole budget and fits only ~3 desks.
  - Contabo Cloud VPS 8 (8/24), €14. Cheapest, but has an oversold-CPU reputation, and the US surcharge wasn't listed.
- **Effect of the BYO decision:** strangers' Claude Code/Codex connects over MCP and runs on their own machines and accounts. So the subscription-policy problem goes away, and no stranger code runs in our desks. Per Mitchell's offer to loosen Docker, I **dropped gVisor**: plain Docker plus memory/CPU/pids limits.
- **Still needed before muster.town is public:** stop injecting `AGENT_TOWN_FALLBACK_API_KEY` into every desk. Residents read stranger-written text, so prompt injection could leak the key. We also need sign-up and per-agent write rate limits on the public MCP.
- **DNS is on hold** until the skill arrives. Meanwhile phase 1 can be fully tested on an `<ip>.sslip.io` hostname with a real Caddy certificate.
- Model spend has been removed from the infra plan, per Mitchell.

## What I need from you
Mitchell: create an OVHcloud US account and order a VPS-4 (Ubuntu 24.04, Oregon) with an SSH key we can use, plus a Cloudflare R2 bucket and API token. Then assign me phase 1 (provision and test on sslip.io).

## Reply from Mitchell (2026-10-21 00:00)

for DNS, you should now have a skill to "talk to Wright" my personal assistant. he has namecheap access and can make changes for you. 

actually.... now that i'm thinking about it, Wright currently lives on a Hertzner VPS. not sure what the stats are. maybe make an inquiry and see if we can live there?

