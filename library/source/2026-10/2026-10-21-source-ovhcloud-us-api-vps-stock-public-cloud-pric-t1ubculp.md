---
id: "dc_v5t1ubculp"
type: "source"
state: "library"
title: "Source: OVHcloud US API: VPS stock, Public Cloud prices and what the API can do (queried 2026-10-21)"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":["https://api.us.ovhcloud.com/1.0/","https://api.us.ovhcloud.com/1.0/order/catalog/public/vps?ovhSubsidiary=US","https://api.us.ovhcloud.com/1.0/order/catalog/public/cloud?ovhSubsidiary=US","https://us.ovhcloud.com/public-cloud/prices/","https://us.ovhcloud.com/public-cloud/regions-availability/","https://support.us.ovhcloud.com/hc/en-us/articles/39499067423379-How-to-order-a-VPS"]}
tags: ["prod","hosting","ovh","api","pricing"]
createdAt: "2026-10-21T17:53:02.506Z"
updatedAt: "2026-10-21T17:53:02.506Z"
---
Queried the public, unauthenticated OVH US API (api.us.ovhcloud.com/1.0) on 2026-10-21. Prices are USD excluding tax.

**VPS stock** (`GET /vps/order/rule/datacenter?ovhSubsidiary=US&planCode=…`):
- vps-2027-model1 (VPS-1, 2 vCPU / 4 GB / 40 GB, $5.35/mo no commitment): Linux **available in US-EAST-VA only**. US-WEST-OR out of stock.
- vps-2027-model2/3/4 (VPS-2/3/4): Linux **out of stock** in US-EAST-VA and US-WEST-OR. The -ca and -eu variants are out of stock in every DC listed (BHS, GRA, SBG, RBX, DE, UK, WAW, MIL).
- Catalog prices (`/order/catalog/public/vps`): VPS-2 $10.00 / VPS-3 $14.50 / VPS-4 $27.50 per month with no commitment, or $8.50 / $12.32 / $23.37 on 12 months.

**Public Cloud catalog** (`/order/catalog/public/cloud?ovhSubsidiary=US`, consumption prices are per hour):
| Flavor | Specs (from the OVH prices page) | Hourly | Monthly billing |
|---|---|---|---|
| d2-8 (Discovery) | 4 vCPU / 8 GB / 50 GB | $0.0461 (≈$33.65/mo) | $25.53 |
| d2-4 | 2 vCPU / 4 GB | $0.0256 | $14.18 |
| b2-7 | 2 vCPU / 7 GB / 50 GB SSD | $0.0879 | $31.19 |
| b3-8 | 2 vCPU / 8 GB, local storage | $0.0605 (≈$44.17/mo) | $37.54 on a 12-month savings plan |
| b3-16 | 4 vCPU / 16 GB | $0.1208 | — |
| r3-16 | 2 vCPU / 16 GB | $0.0783 | — |
The prices page says outbound traffic is included outside APAC. The regions page lists US Public Cloud in Seattle/Hillsboro and Washington DC (Vint Hill). **Which flavors each US region offers isn't public**: it needs `GET /cloud/project/{id}/flavor?region=…` with a token.

**What the US API covers** (`GET /1.0/` lists the sections): /cloud (598 endpoints: instance create/delete/resize/reinstall/rescue/shelve/snapshot, SSH keys, volumes, networks, object storage, managed DBs, Kubernetes), /vps (manage an existing VPS: reboot, rebuild, snapshots, backups, IPs, console, terminate, but not create one), /order (cart-based ordering of any product), /domain, /ip, /me. Auth is an application key + secret + consumer key, and the consumer key can be limited to paths such as `/cloud/project/<id>/*`.
