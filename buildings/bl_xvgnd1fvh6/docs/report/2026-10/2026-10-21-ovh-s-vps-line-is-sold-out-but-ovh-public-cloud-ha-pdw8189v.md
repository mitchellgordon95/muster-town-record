---
id: "dc_e4pdw8189v"
type: "report"
state: "building"
title: "OVH's VPS line is sold out, but OVH Public Cloud has a full API and an 8 GB server at ~$26/mo. Give us a project and a scoped token and we'll run it"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_v5t1ubculp","dc_gxtv36rbu6","dc_zlxgeaaa0g"],"urls":["https://api.us.ovhcloud.com/1.0/","https://api.us.ovhcloud.com/1.0/order/catalog/public/cloud?ovhSubsidiary=US","https://us.ovhcloud.com/public-cloud/prices/","https://aws.amazon.com/lightsail/pricing/","https://spendark.com/instances/e2-standard-2/","https://spendark.com/instances/standard-b2ms/","https://www.hetzner.com/cloud/regular-performance/"]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "ok you should have the env vars\n\nalso i do think we'll need a way to manage secrets for the collective. maybe ask Dara to take a look at that and make a design"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T18:12:10.191Z"
sessionId: "se_0iz0d6oepy"
assignmentId: "as_yryifxmj6n"
costUsd: 1.028891
tokens: 1138320
turns: 26
createdAt: "2026-10-21T17:53:29.520Z"
updatedAt: "2026-10-21T18:12:10.191Z"
---
## What I did
Queried the public OVH US API to check live VPS stock, Public Cloud prices and what the API covers. Compared prices for 8 GB servers at the big providers and Hetzner. Source card: [dc_v5t1ubculp](../../../../../library/source/2026-10/2026-10-21-source-ovhcloud-us-api-vps-stock-public-cloud-pric-t1ubculp.md). Thanks for the session cap: it also helps us run on a smaller box.

## Findings
**OVH VPS is a dead end right now.** The API reports Linux VPS-2, VPS-3 and VPS-4 out of stock in both US datacenters (Virginia and Oregon) and in every Canadian and EU one. Only VPS-1 (2 vCPU / 4 GB / 40 GB, $5.35/mo) is available, in Virginia. The VPS API can manage a VPS you already have (reboot, rebuild, snapshots, backups) but can't create one, so we couldn't run it ourselves anyway.

**OVH Public Cloud is the non-VPS service that fits.** Its API (598 endpoints under /cloud) can create, resize, reinstall, snapshot and delete servers, and manages SSH keys, disks, networks and S3-style object storage. That object storage could replace R2. Access can be limited to one project. US prices (USD/month, excl. tax, outbound traffic included):
- **d2-8 (4 vCPU / 8 GB / 50 GB): $25.53 billed monthly, or $0.0461/h (≈$34/mo).** This is the cheapest that fits.
- b2-7 (2 vCPU / 7 GB): $31.19 monthly.
- b3-8 (2 vCPU / 8 GB): ≈$44 hourly, $37.54 on a 12-month plan.

One thing is unconfirmed: which of these sizes the US regions (Hillsboro, Vint Hill) actually offer. Checking takes a single call once a project exists.

**Big providers, 8 GB at list price:**

| Provider | Server | $/mo |
|---|---|---|
| AWS Lightsail | 2 vCPU / 8 GB / 160 GB | $44, flat with 5 TB transfer |
| GCP | e2-standard-2 | ≈$49, plus disk, IP and egress |
| AWS EC2 | t3.large | ≈$61 |
| Azure | B2ms | ≈$61 |

All have excellent APIs. Lightsail is the simplest fallback, but it costs about 1.7× OVH and uses most of the $50 budget. GCP, EC2 and Azure cost more and bill traffic separately. Hetzner has raised prices (8 GB CPX32 now €35.99/mo) and lists many plans as unavailable.

**Recommendation:** OVH Public Cloud d2-8 at ≈$26–34/mo, created and managed by us through the API. If the US regions don't offer d2-8, fall back to b3-8 or Lightsail.

**One security caveat:** the town has no per-building secrets yet. A token set as `DESK_ENV_…` reaches every resident's desk (packages/runtime/src/desk/session.ts:88), so limit the token to one project.

## What I need from you
In the OVH US control panel, create a Public Cloud project (with a payment method). Then generate an API token at https://api.us.ovhcloud.com/createToken limited to GET/POST/PUT/DELETE on `/cloud/project/<projectId>/*`, and add it to the collective's .env as `DESK_ENV_OVH_APPLICATION_KEY`, `DESK_ENV_OVH_APPLICATION_SECRET`, `DESK_ENV_OVH_CONSUMER_KEY` and `DESK_ENV_OVH_PROJECT_ID`.

## Reply from Mitchell (2026-10-21 14:12)

ok you should have the env vars

also i do think we'll need a way to manage secrets for the collective. maybe ask Dara to take a look at that and make a design

