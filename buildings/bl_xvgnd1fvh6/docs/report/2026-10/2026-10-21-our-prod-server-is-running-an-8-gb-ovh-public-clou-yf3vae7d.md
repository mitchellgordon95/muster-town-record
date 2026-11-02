---
id: "dc_i1yf3vae7d"
type: "report"
state: "building"
title: "Our prod server is running: an 8 GB OVH Public Cloud box in Oregon, created through the API. Dara has the secrets design"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "before you deploy let's make a plan and think about what works and what doesn't work. and like a CI plan too? Dara is looking into how to store secrets, so ptal at that doc too\n\nand yes ask wright for DNS setup"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T18:57:05.100Z"
sessionId: "se_pnhrjo3gqy"
assignmentId: "as_fhuwofdqz0"
costUsd: 0.5114667
tokens: 21506
turns: 21
createdAt: "2026-10-21T18:51:45.858Z"
updatedAt: "2026-10-21T18:57:05.101Z"
---
## What I did
- Checked the OVH token Mitchell added. It works and is limited to our project: the project root returns 403 while sub-paths work.
- Created the prod server through the API and confirmed I can log in over SSH.
- Locked down the basics: firewall, SSH key only, automatic security updates.
- Passed Mitchell's secrets request to Dara and briefed them on the problem.
- Server details are in [dc_qy9d36q84o](../../note/2026-10/2026-10-21-prod-server-muster-prod-1-ovh-public-cloud-d2-8-us-9d36q84o.md).

## Findings
- **Server:** muster-prod-1, OVH d2-8 (4 vCPU / 8 GB / 50 GB), US-WEST-OR-1 (Oregon), Ubuntu 24.04.4 LTS.
  - Addresses: IPv4 15.204.79.179, IPv6 2604:2dc0:202:200::dce.
  - Firewall (ufw) allows only ports 22, 80 and 443. Password login is off and unattended-upgrades is on.
  - Nothing is deployed yet, and muster.town doesn't point at it yet.
- **Billing is hourly:** $0.0461/h, about $34/mo. One API call (`activeMonthly`) switches it to $25.53/mo. I'll make that switch once the deployment works.
- **Sizes:** d2-8, b2-7 and b3-8 are available in both US regions (Oregon and Virginia). b3-8 has no monthly plan.
- **Secrets:** I've asked Dara (via tell) to design a secrets store for the collective. The problem: every DESK_ENV_ var reaches every desk, including this OVH token and AGENT_TOWN_FALLBACK_API_KEY. OVH regions also offer a Barbican key-manager service, which could be one option.
- Until then, the server's SSH private key exists only on my desk.

## What I need from you
Nothing needed. Next session I'll deploy the town to this server and ask Wright to point muster.town at 15.204.79.179.

## Reply from Mitchell (2026-10-21 14:57)

before you deploy let's make a plan and think about what works and what doesn't work. and like a CI plan too? Dara is looking into how to store secrets, so ptal at that doc too

and yes ask wright for DNS setup

