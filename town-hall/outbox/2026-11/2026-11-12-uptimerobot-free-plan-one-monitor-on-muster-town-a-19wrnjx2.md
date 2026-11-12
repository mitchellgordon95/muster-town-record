---
id: "dc_8319wrnjx2"
type: "request"
state: "building"
title: "UptimeRobot free plan: one monitor on muster.town, a status page, and two secrets pasted at Town Hall → Secrets"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["data"]
requestStatus: "done"
claimedByUserId: "us_1la74k332n"
createdAt: "2026-11-12T14:42:31.046Z"
updatedAt: "2026-11-12T17:31:35.756Z"
---
You chose UptimeRobot's free plan over a pinger agent today (your 1:1 with Secretary, decision 3). Prod has filed the grant; its step 2 needs these from you. About 6 screens, once:

1. Sign up at https://uptimerobot.com (free plan) and verify your email.
2. Add New Monitor → HTTP(s) → URL `https://muster.town/api/health`, interval 5 minutes, alert contact your email. One process serves the Workshop and every hosted collective, so one monitor covers all of them.
3. Status Pages → New status page → pick that monitor → save. Copy its public URL (uptimerobot's own domain; a custom domain is not on the free plan).
4. Integrations & API → API keys → create a **Read-only API key**. It can only read what the status page already shows publicly.
5. At muster.town → Town Hall → Secrets, paste two collective secrets: `UPTIMEROBOT_API_KEY` = the read-only key, `UPTIMEROBOT_STATUS_URL` = the status page URL. Never paste the key anywhere else (not in a chat, not in this request).
6. Answer this request "done". Step 2 reads both from the secrets store (as FLY_DESKS_ACCESS_TOKEN does); nothing else is needed.

Free-plan limits (uptimerobot.com/pricing, read 2026-11-12): 50 monitors, 5-min interval, 1 status page, 3 months of data, API at 10 req/min. SMS alerts cost extra; email alerts are enough. Caveat: at a 5-min interval our seconds-long restarts will mostly not show as downtime; the block keeps listing restart gaps from the server's own events.

If you send only the status page URL (no key), the block links the page and shows no number.
