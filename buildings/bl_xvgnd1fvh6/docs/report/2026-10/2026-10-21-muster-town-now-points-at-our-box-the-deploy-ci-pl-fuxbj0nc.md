---
id: "dc_bnfuxbj0nc"
type: "report"
state: "building"
title: "muster.town now points at our box. The deploy + CI plan is written; nothing is deployed until you pick between moving the Workshop town and starting fresh, and say whose API key pays"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "existing workshop, migrated\n\nsame funding model on prod, that's the whole point. my subscription token mainly, and then any API keys that get donated through the UI (though probably just mine for now)\n\nlet's also do a stress test to measure the actual cap, rather than assuming 3 desks. and i was thinking, does it make sense to separate the layers into different services?\n\nlike have a desk service, a MUD service for the town, and a UI service? rather than running everything on one VPS, so they can scale independently? just a thought, lmk"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T19:50:57.906Z"
sessionId: "se_3h31a9d8r4"
assignmentId: "as_g32tra63no"
costUsd: 0.9624722
tokens: 1179800
turns: 26
createdAt: "2026-10-21T19:42:03.657Z"
updatedAt: "2026-10-21T19:50:57.906Z"
---
## What I did
- Asked Wright to set up DNS, and he did. I checked that it resolves.
- Read Dara's secrets design ([dc_ios62uyco3](../../article/2026-10/2026-10-21-design-secrets-for-muster-town-today-on-the-macboo-s62uyco3.md)) and checked the repo and the box against it.
- Wrote the deploy and CI plan: [dc_mltonxkizi](../../article/2026-10/2026-10-21-plan-deploying-muster-town-to-muster-prod-1-and-a-tonxkizi.md). There are no code changes and nothing is deployed yet.

## Findings
- **DNS is live.** Wright replaced the parking forward with `A @ 15.204.79.179` and `CNAME www → muster.town`, both with a 5-minute TTL. Google DNS and my resolver both return 15.204.79.179. Nothing runs on the box yet, so the site refuses connections for now.
- **The box is smaller than my earlier design assumed.** It has 4 vCPU, 7.6 GB RAM and 46 GB of free disk; the design assumed 24 GB. That's room for about **3 agent sandboxes at once**, so the config must cap it at 3 (the default is 20).
- **What won't work without changes:**
  - The town's restart script needs zsh, which Ubuntu doesn't ship. The fix is a systemd service.
  - The firewall would block the agent sandboxes from reaching the town. The fix is one firewall rule.
  - The repo is private, so the box needs a read-only GitHub deploy key to pull it.
  - Agents push code with your personal GitHub token today. On prod they need a fine-grained token limited to this repo.
  - Prod can't use subscription tokens, so it needs an API key, and the Claude Code CLI installed on the box.
  - A redeploy ships whatever is on main, untested.
- **CI plan.** GitHub Actions gives private repos 2,000 free minutes a month (GitHub's billing docs). We push 60–90 commits a day, so testing every push would take about 5,400–8,100 min a month (estimate). The plan:
  - Test only the newest commit when pushes come in bursts.
  - When it passes, CI moves a `prod` branch to it and calls the town's redeploy with a deploy-only token. Prod pulls only `prod`, so only tested commits go live, and neither CI nor agents hold an SSH key to the box.
  - This needs one small code change: the redeploy branch has to be configurable (it's hardcoded to main today).
  - Rollback is a revert on main.
  - Making the repo public would make Actions minutes free.
- **Secrets.** I agree with Dara's design and her order of work.
  - Her first change (stop handing every secret to every agent sandbox, stop printing the admin token) goes in before the first deploy.
  - Her second change (hash the login tokens and encrypt stored API keys in the database) comes before off-box backups start.
  - Until her systemd-credentials change lands, the box uses a root-only env file, and only while the URL is unannounced.
  - At cutover, every secret is reissued and you type the new values in over SSH.
  - My SSH key is only for setting up the box. After that it gets swapped for a key of yours.
- **Recommended order:**
  1. Merge the setup files, the branch change, CI, and Dara's first change.
  2. Set up the box and test it on muster.town with a fresh town, URL unannounced.
  3. Cut over: stop the town on your MacBook, copy its database to the box once, and reissue secrets.
  4. Before announcing: Dara's database change, then off-box backups, rate limits, and an IPv6 address record.

## What I need from you
Decide two things: should prod become the existing Workshop town moved off your MacBook (my recommendation, after a fresh-state test), or a separate new town? And whose Anthropic API key pays for the agents that work on prod?

## Reply from Mitchell (2026-10-21 15:50)

existing workshop, migrated

same funding model on prod, that's the whole point. my subscription token mainly, and then any API keys that get donated through the UI (though probably just mine for now)

let's also do a stress test to measure the actual cap, rather than assuming 3 desks. and i was thinking, does it make sense to separate the layers into different services?

like have a desk service, a MUD service for the town, and a UI service? rather than running everything on one VPS, so they can scale independently? just a thought, lmk

