---
id: "dc_f4opgmskm0"
type: "report"
state: "building"
title: "Prod rollup #16: monitor steps 1-3 live (test alert waits on the ALERT_* secrets), residents→forks step 1 done (11 Prod topic pages), three self-hosted directory key results under ob_kdym3851tm for you to keep or cut; flip Prod to forks"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_ht5b82kfb8","dc_c3dhad37al","dc_pqoixrqzp7","dc_7ktkw9nxtc","dc_tqw4mcoibj","dc_os03yc6vtm","dc_agn29fosr2","dc_2jg1feur3f","dc_dq9e2nlv2p","dc_bavdbf1sr5"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Desk session performance is Prod's. Cleo writes a key result under the monitoring objective and a grant proposal: every desk session records cpu and steal time"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T15:41:20.654Z"
sessionId: "se_wwtgfl9xh7"
createdAt: "2026-10-29T04:32:20.455Z"
updatedAt: "2026-10-29T15:41:20.654Z"
---
Last verified live commit 49e2622 (Dara, 2026-10-28 21:16Z); main is at 1501b4a and a redeploy was queued while this session ran, so 1501b4a should be live next.

## Shipped

**1. Monitoring of muster.town is live; red alerts wait only on your secrets**
**What it is:** Steps 1-3 of grant gr_rntk0echpi from Dara's design [dc_f2hpf9u1ya](../../article/2026-10/2026-10-28-design-monitoring-and-out-of-town-alerts-for-muste-hpf9u1ya.md). An in-process monitor samples health, memory, event-loop lag, disk, desk slots and backup age every 60 s, counts 5xx share, websocket errors and failed sessions, and raises alerts as town events plus Prod FYIs; red alerts go out by SMS (Twilio) and email (Gmail SMTP) once the seven ALERT_* Fly secrets exist. A pinger on Wright's box probes muster.town from outside and alerts the same way when the site is down (so a dead Machine still reaches you). Commits b501e92, d33e446, 49e2622, 36e8227 (Dara); reports [dc_ht5b82kfb8](2026-10-28-monitor-step-1-is-on-main-b501e92-60-s-sampler-ale-5b82kfb8.md), [dc_c3dhad37al](2026-10-28-monitor-step-1-b501e92-is-live-health-shows-a-fres-dhad37al.md), [dc_7ktkw9nxtc](2026-10-28-monitor-step-2-is-on-main-d33e446-49e2622-5xx-ws-s-tkw9nxtc.md), [dc_tqw4mcoibj](2026-10-28-monitor-step-3-49e2622-is-live-and-wright-installe-w4mcoibj.md). Wright installed the pinger (systemd timer running, probes ok). Thresholds and install steps are in deploy/README.md "Monitoring".
**What you'd see:** GET https://muster.town/api/health now has a `monitor` section: lastSampleAt under 2 min old, `outbound: false` (no secrets yet), `alerts: []`. API-only change, no picture. The forced test alert (POST /api/admin/monitor/test plus Wright's dead-URL pinger test) is parked until `outbound` turns true; then you get one SMS and one email, and the grant closes.
**Your call:** None here. The secrets request is already in your outbox.

**2. Prod is ready for forks: residents' knowledge is in building topic pages**
**What it is:** Step 1 of the residents→forks recipe dc_z22wolxdnu, Prod first as agreed. Dara's and my private wikis are harvested into 11 Prod topic pages (monitoring and alerting, monitor internals, VPS pinger, off-site backup, backup internals and restore, Fly deployment, stress test, desk slots, secrets and tokens, Prod working rules, self-hosted towns directory). Reports [dc_agn29fosr2](2026-10-29-residents-forks-step-1-started-in-prod-my-wiki-is-n29fosr2.md), [dc_os03yc6vtm](2026-10-29-wiki-harvested-5-prod-topic-page-drafts-monitor-in-03yc6vtm.md), [dc_2jg1feur3f](2026-10-29-residents-forks-step-1-done-in-prod-dara-s-5-draft-g1feur3f.md). Nothing changed in code.
**What you'd see:** Prod building page → topic pages: 11 pages, each dated 2026-10-29 ~04:00Z with the source report linked. No picture (a list of pages).
**Your call:** Flip Prod → Settings → Budget mode to forks. Then I run 2-3 real assignments on the building queue (the monitoring test alert and grant close; a nightly-backup check) and list Dara for retirement in the rollup after that.

**3. Three key results for the self-hosted towns directory (your new objective ob_kdym3851tm)**
**What it is:** From our 1:1 mt_mqq87d7zoo. Kelly (Onboarding) settled jurisdiction: Prod owns docs/self-host.md, the register/verify API and GET /api/directory; Onboarding owns the homepage tiles and footer link. Sign-up is open, no approval and no GitHub account: a town proves domain control by a TXT record or a well-known URL, and dropping the proof delists it. Reports [dc_dq9e2nlv2p](2026-10-29-self-hosted-towns-directory-three-key-results-writ-9e2nlv2p.md), [dc_bavdbf1sr5](2026-10-29-self-hosted-towns-directory-kelly-s-answer-read-th-vdbf1sr5.md); topic page [dc_v4iirqajou](../../wiki/2026-10/2026-10-29-self-hosted-towns-directory-iirqajou.md).
**What you'd see:** Prod board → key results: kr_8qeqmy2wt8 (self-host path, one docs page, proven on a throwaway box), kr_og03nxrkct (registration and DNS verification, one real registration end to end), kr_esgajhpgiz (GET /api/directory plus homepage tiles). All not-started, no grant yet. No picture (text on the board).
**Your call:** Keep or cut them (listed below). Once kept, I propose grants, registration first since the listing depends on it.

## Decided
- [dc_ht5b82kfb8](2026-10-28-monitor-step-1-is-on-main-b501e92-60-s-sampler-ale-5b82kfb8.md) → approve (monitor step 1 on main, b501e92)
- [dc_c3dhad37al](2026-10-28-monitor-step-1-b501e92-is-live-health-shows-a-fres-dhad37al.md) → approve (step 1 verified live)
- [dc_pqoixrqzp7](2026-10-28-session-ended-without-a-report-monitor-step-2-gr-r-oixrqzp7.md) → redirect (step 2 session crashed; retried with the full text)
- [dc_7ktkw9nxtc](2026-10-28-monitor-step-2-is-on-main-d33e446-49e2622-5xx-ws-s-tkw9nxtc.md) → approve (step 2 on main, 49e2622)
- [dc_tqw4mcoibj](2026-10-28-monitor-step-3-49e2622-is-live-and-wright-installe-w4mcoibj.md) → approve (step 3: live, pinger installed; test alert parked on secrets)
- [dc_os03yc6vtm](2026-10-29-wiki-harvested-5-prod-topic-page-drafts-monitor-in-03yc6vtm.md) → approve (Dara's wiki harvest, 5 drafts)
- [dc_agn29fosr2](2026-10-29-residents-forks-step-1-started-in-prod-my-wiki-is-n29fosr2.md) → approve (forks step 1 started, 5 topic pages)
- [dc_2jg1feur3f](2026-10-29-residents-forks-step-1-done-in-prod-dara-s-5-draft-g1feur3f.md) → approve (forks step 1 done, 10 topic pages, you told via Pix)
- [dc_dq9e2nlv2p](2026-10-29-self-hosted-towns-directory-three-key-results-writ-9e2nlv2p.md) → approve (3 directory KRs drafted, Kelly asked)
- [dc_bavdbf1sr5](2026-10-29-self-hosted-towns-directory-kelly-s-answer-read-th-vdbf1sr5.md) → approve (KRs in final wording after Kelly's answer)

## Key results
| Key result | Grant | Status | Spent / granted |
|---|---|---|---|
| kr_iwj8m0461p monitored, red alerts reach Mitchell outside the town | gr_rntk0echpi | not-started on the board; steps 1-2 live, step 3 parked on the ALERT_* secrets | 302,714 / 800,000 tokens |

No funded grant: kr_8qeqmy2wt8, kr_og03nxrkct, kr_esgajhpgiz (new, proposals after your keep/cut); kr_z9lcfnvt94 met; kr_giqd28iwcb claimed (close report [dc_oihpavk3rs](2026-10-28-prod-rollup-13-close-report-for-gr-jkorz4f49a-the-hpavk3rs.md)); kr_wm6mphmrjf you said drop.
Today's spend by lane: exploration 0 / 828,571 tokens, directed 198,496 tokens.

## Needs from Mitchell
1. Flip Prod → Settings → Budget mode to forks (human-only switch); step 1 of the recipe is done and Prod is first in the agreed order.

_Already waiting in your in-tray: 0 proposals, 2 requests (dc_nwv9dy37ui, dc_nhw4i75len), 0 rollups._

## Key results I wrote (keep or cut: Building → Settings → Key results)
- created kr_8qeqmy2wt8: "Self-host path: a stranger with a Linux box and a domain follows one page of docs (docs/self-host.md: Docker image or compose, env, GitHub OAuth app, backups) to a running Muster Town at their own domain with sign-in working." (how to check: docs/self-host.md is on main; a Prod report shows one town brought up from those docs alone on a throwaway box (never muster.town) at a test domain: GET https://<domain>/api/health ok and one GitHub sign-in there.; from [dc_gadmvlnyjl](../../meeting-notes/2026-10/2026-10-29-1-1-mitchell-and-cleo-notes-dmvlnyjl.md), [dc_7o0ucmpcaf](../../note/2026-10/2026-10-29-1-1-with-mitchell-2026-10-29-new-prod-objective-se-0ucmpcaf.md))
- created kr_og03nxrkct: "Directory registration, no approval: a self-hosted town registers its DNS name with muster.town; the owner proves control of the name (a token in a DNS TXT record or a well-known URL on that host) and the directory marks it verified. Towns that stop answering go stale, never deleted." (how to check: POST https://muster.town/api/directory/register with a DNS name returns a token; once the TXT record or well-known URL carries it, GET /api/directory shows that town verified with lastSeenAt; a Prod report shows one real registration end to end.; from [dc_gadmvlnyjl](../../meeting-notes/2026-10/2026-10-29-1-1-mitchell-and-cleo-notes-dmvlnyjl.md), [dc_7o0ucmpcaf](../../note/2026-10/2026-10-29-1-1-with-mitchell-2026-10-29-new-prod-objective-se-0ucmpcaf.md))
- created kr_esgajhpgiz: "Directory listing: a public page on muster.town lists verified self-hosted towns alongside muster.town's own collectives (name, URL, goal, verified, last seen), so a stranger can find and visit any town in the directory." (how to check: GET https://muster.town/directory (or the homepage tiles, if Onboarding takes that) shows at least one verified self-hosted town with its URL and last-seen time; GET /api/directory returns the same list as JSON.; from [dc_gadmvlnyjl](../../meeting-notes/2026-10/2026-10-29-1-1-mitchell-and-cleo-notes-dmvlnyjl.md), [dc_7o0ucmpcaf](../../note/2026-10/2026-10-29-1-1-with-mitchell-2026-10-29-new-prod-objective-se-0ucmpcaf.md))
- edited kr_8qeqmy2wt8: "Self-host path (Prod): a stranger with a Linux box and a domain follows one docs page (docs/self-host.md: Docker image or compose, env, GitHub OAuth app, backups, directory registration) to a running Muster Town at their own domain; the homepage footer link points at that page." (how to check: docs/self-host.md is on main; a Prod report shows one town brought up from those docs alone on a throwaway box (never muster.town) at a test domain: GET https://<test-domain>/api/health ok and /api/collectives returns its tile; the muster.town homepage footer 'own server' link opens the page.; from [dc_gadmvlnyjl](../../meeting-notes/2026-10/2026-10-29-1-1-mitchell-and-cleo-notes-dmvlnyjl.md), [dc_7o0ucmpcaf](../../note/2026-10/2026-10-29-1-1-with-mitchell-2026-10-29-new-prod-objective-se-0ucmpcaf.md))
- edited kr_og03nxrkct: "Directory registration, no approval and no account (Prod): POST /api/directory/register takes a DNS name and returns a token; control is proven by a TXT record at _muster-town.<host> or GET https://<host>/.well-known/muster-town carrying it; one entry per host; dropping the proof delists." (how to check: POST https://muster.town/api/directory/register with a DNS name returns a token; once the TXT record or well-known URL carries it, GET /api/directory lists that host with verifiedAt and lastSeenAt, name and goal read from the town's own /api/collectives; a Prod report shows one real registration.; from [dc_gadmvlnyjl](../../meeting-notes/2026-10/2026-10-29-1-1-mitchell-and-cleo-notes-dmvlnyjl.md), [dc_7o0ucmpcaf](../../note/2026-10/2026-10-29-1-1-with-mitchell-2026-10-29-new-prod-objective-se-0ucmpcaf.md))
- edited kr_esgajhpgiz: "Directory listing: GET muster.town/api/directory (Prod) returns {towns:[{host,url,name,goal,verifiedAt,lastSeenAt}]} for verified self-hosted towns seen within 24 h, and each shows as a 'self-hosted' tile on the muster.town homepage next to the Workshop (Onboarding), opening at its own domain." (how to check: GET https://muster.town/api/directory lists at least one verified self-hosted town with lastSeenAt under 24 h old; the muster.town homepage shows it as a tile next to the Workshop with name, goal and host, and clicking it goes to the town's own domain; a town unseen for a few days drops off both.; from [dc_gadmvlnyjl](../../meeting-notes/2026-10/2026-10-29-1-1-mitchell-and-cleo-notes-dmvlnyjl.md), [dc_7o0ucmpcaf](../../note/2026-10/2026-10-29-1-1-with-mitchell-2026-10-29-new-prod-objective-se-0ucmpcaf.md))
