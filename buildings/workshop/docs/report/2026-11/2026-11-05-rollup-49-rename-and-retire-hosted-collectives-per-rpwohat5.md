---
id: "dc_rvrpwohat5"
type: "report"
state: "building"
title: "Rollup 49: rename and retire hosted collectives + per-collective stats, a bulletin board for humans in the town square, and a tidier Town Hall (one-line digest, outbox tabs with withdraw/decline, mod station = bans)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_i6t3qu137c","dc_ulthxi1ezu","dc_tmsebn3gs9","dc_9olxq5gp3u","dc_7veh9cvk29","dc_wiix83b31l","dc_5zbsl91xvc","dc_9ajkoiwrrl","dc_794fbtskv9","dc_mlr5w1kyv7","dc_4q13q3rjao","dc_xahk1cf13m","dc_17h2et0eo6","dc_4ixl7f7w39","dc_ndrq45u12n","dc_buvi0w5wdz","dc_7plxth8ddm","dc_sgf89f4lh7","dc_htsz53fhkz","dc_mpdta8zt8w","dc_uvfxbcx3jb","dc_f8v8faa3yd","dc_jd5r85btnp","dc_1oueiorzcf","dc_jqwwluqnm2","dc_ngffrnhtc0","dc_j4epcdr6a5","dc_zgbcla6udu","dc_bey780gdew","dc_04ok6ashf9","dc_3p77kqogs4","dc_t0qjvmx9gf","dc_8ti3uzwyc1","dc_v5xjviwcui","dc_2dkm8n1r5i","dc_t2lywyu8xu","dc_8nik9gnprz","dc_5g0iji1ww7"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/355","https://github.com/mitchellgordon95/muster-town/pull/353","https://github.com/mitchellgordon95/muster-town/pull/361","https://github.com/mitchellgordon95/muster-town/pull/357","https://github.com/mitchellgordon95/muster-town/pull/359","https://github.com/mitchellgordon95/muster-town/pull/358","https://github.com/mitchellgordon95/muster-town/pull/367","https://github.com/mitchellgordon95/muster-town/pull/360"]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_4en7j5yx5d"
createdAt: "2026-11-05T21:00:20.107Z"
updatedAt: "2026-11-05T21:00:20.107Z"
---
Live: edd5da0 since 20:52 UTC (every item below is on it; PR #369 = bcea003e is merged but not live yet).

## Shipped

**1. Hosted collectives: rename one, retire one, and User stats now show that collective's own engagement**
**What it is:** Both pieces of your flag [dc_hz1nz88pkt](../../flag/2026-11/2026-11-05-i-d-like-to-be-able-to-rename-my-collective-1nz88pkt.md). A collective's name can change while its slug stays (PR #355 = 70fdca4: Planning desk → System → This collective → Rename). A hosted collective can be retired for good (PR #353 = dc1fcbf: its page goes 410, it leaves the homepage, the slug is never reused, files and backups stay on disk). And your flag [dc_r7u6bkaei4](../../flag/2026-11/2026-11-05-user-stats-panel-in-the-workshop-should-show-stats-u6bkaei4.md) piece 1: the User stats panel opens on "This collective, last 30 days" (PR #361 = cd1adc86, GET /api/engagement) instead of the summed Muster Town funnel; on the Workshop only, the old funnel is folded underneath.
**What you'd see:** muster.town/workshop/ → Town Hall → User stats: 9 tiles (live at 20:49Z: Humans 2, Spoke 590, 1:1s 109, Flags 31, Decisions 454, Asked / Let in / Declined / Acted 0), Typical wait, By day. Picture mf_9vj71skfml in [dc_7veh9cvk29](2026-11-05-live-checked-town-hall-user-stats-opens-on-this-co-eh9cvk29.md). Nothing has been renamed or retired yet: both are your clicks.
**Your call:** Do the two clicks: muster.town/trauma/ → Town Hall → Planning desk → System → This collective → "Trauma Town" → Rename; and muster.town/workshop → Planning desk → System → Hosted collectives → Retire… next to Hollyville.

**2. A bulletin board for humans in the town square**
**What it is:** Your flag [dc_52njv3shp8](../../flag/2026-11/2026-11-05-can-i-get-a-bulletin-board-outside-the-town-hall-f-njv3shp8.md). A free-standing board three tiles left of the Town Hall door (PR #357 = 534c57ee). Any signed-in human posts a note (agents get 403); the author or an admin takes one down; E at the board opens the panel. Doc type `bulletin`, GET/POST /api/bulletin.
**What you'd see:** Walk to the board by the Town Hall door and press E; the panel lists notes and has a compose box when you are signed in.
![bulletin board on the map](/api/media/mf_lgfb1dvxxd.png)
**Your call:** Post one note as yourself. Desks have no GitHub sign-in, so a real signed-in post is the one check the forks could not make; if it fails, say so in a flag.

**3. Town Hall tidy: the digest is one in-tray row, the Outbox has tabs with withdraw and decline, the mod station is bans only, and the Planner and Secretary rest where they work**
**What it is:** Four of your asks from today's 1:1s and flag. The daily digest is one clickable line in the in-tray that opens the digest doc (PR #359 = 83ce5011; the Approve-all for overtaken rollups sits under the opened doc). Outbox requests get Pending / Claimed / Done tabs; an author withdraws its own request with a note, a new request can replace an older one, and you can decline one by saying "decline dc_…" to the Secretary in a 1:1 (PR #367 = edd5da04; delete stays admin-only). The mod station's duplicate Requests tab is gone; the old link opens the Outbox (PR #358 = b0ce742d). The Planner idles by the goal tree and the Secretary by the in-tray (PR #360 = 6007c2d3).
**What you'd see:** Town Hall in-tray: a "Digest · by the Secretary" section with one row ("Digest 2026-11-05: 18 decisions, 4 rollups"); click opens it. Outbox: three tabs (6 requests were open at 20:08Z). Mod station: "Banning is for admins" + Recent bans only.
![digest row in the in-tray](/api/media/mf_8s24fpezmv.png)
**Your call:** None. (The buildings withdraw their own stale "test this for us" requests now that withdraw is live; Pix 2 is clearing the Workshop's four as this files.)

## Decided
- [dc_i6t3qu137c](2026-11-05-grant-a-gr-9kt5t7w51w-funded-1m-cut-into-3-steps-s-t3qu137c.md) → approve (grant A gr_9kt5t7w51w cut into 3 steps; step 1 as_qug2qgx7pl running on Pix 1)
- [dc_ulthxi1ezu](2026-11-05-live-the-digest-is-a-one-line-town-hall-in-tray-ro-thxi1ezu.md), [dc_tmsebn3gs9](2026-11-05-pr-359-merged-83ce5011-digest-as-one-in-tray-line-sebn3gs9.md), [dc_9olxq5gp3u](2026-11-05-pr-359-digest-as-one-in-tray-line-was-conflicting-lxq5gp3u.md) → approve (digest row live, PR #359)
- [dc_7veh9cvk29](2026-11-05-live-checked-town-hall-user-stats-opens-on-this-co-eh9cvk29.md), [dc_wiix83b31l](2026-11-05-user-stats-pr-361-merged-cd1adc86-live-screenshot-ix83b31l.md), [dc_5zbsl91xvc](2026-11-05-user-stats-pr-361-conflicts-with-main-resolved-492-bsl91xvc.md), [dc_9ajkoiwrrl](2026-11-05-user-stats-pr-361-ci-red-manual-md-1-word-over-cap-jkoiwrrl.md), [dc_794fbtskv9](2026-11-05-user-stats-engagement-per-collective-pr-361-open-p-4fbtskv9.md) → approve (User stats per collective, PR #361)
- [dc_mlr5w1kyv7](2026-11-05-mod-station-is-bans-only-and-the-outbox-is-on-its-r5w1kyv7.md), [dc_4q13q3rjao](2026-11-05-pr-358-merged-b0ce742d-parked-on-its-deploy-for-li-13q3rjao.md), [dc_xahk1cf13m](2026-11-05-pr-358-was-red-on-an-unused-export-fixed-parked-on-hk1cf13m.md), [dc_17h2et0eo6](2026-11-05-mod-station-ban-tab-vs-outbox-pr-358-removes-the-s-h2et0eo6.md) → approve (mod station bans only, PR #358)
- [dc_4ixl7f7w39](2026-11-05-planner-secretary-rest-spots-live-planner-by-the-g-xl7f7w39.md), [dc_ndrq45u12n](2026-11-05-planner-secretary-rest-spots-pr-360-merged-6007c2d-rq45u12n.md), [dc_buvi0w5wdz](2026-11-05-planner-secretary-rest-spots-pr-360-open-parked-on-vi0w5wdz.md) → approve (rest spots, PR #360)
- [dc_7plxth8ddm](2026-11-05-pr-367-merged-edd5da04-outbox-withdraw-decline-pen-lxth8ddm.md), [dc_sgf89f4lh7](2026-11-05-pr-367-conflicted-with-main-after-359-resolved-hea-f89f4lh7.md), [dc_htsz53fhkz](2026-11-05-outbox-requests-author-withdraw-replaces-human-dec-sz53fhkz.md), [dc_mpdta8zt8w](2026-11-05-juno-s-relay-for-mitchell-acknowledged-mit-licence-dta8zt8w.md) → approve (outbox withdraw/decline/tabs, PR #367; MIT licence 073ca10 acknowledged, Juno's rollup carries it)
- [dc_uvfxbcx3jb](2026-11-05-pr-369-merged-bcea003e-decisions-naming-a-forking-fxbcx3jb.md), [dc_f8v8faa3yd](2026-11-05-pr-369-was-green-but-main-had-moved-overlap-in-cor-v8faa3yd.md), [dc_jd5r85btnp](2026-11-05-decisions-naming-a-forking-manager-go-to-its-build-5r85btnp.md), [dc_1oueiorzcf](2026-11-05-mara-1-s-question-for-mitchell-answered-as-9512zq0-ueiorzcf.md) → approve (PR #369 = bcea003e merged: decisions naming a forking manager go to its building queue; live check as_9qbjqu1fxy waits on its deploy; no wider routing change until Code Legibility's map is filed)
- [dc_jqwwluqnm2](2026-11-05-collective-rename-merged-pr-355-70fdca4-live-once-wwluqnm2.md), [dc_ngffrnhtc0](2026-11-05-collective-rename-pr-355-had-a-conflict-with-353-m-ffrnhtc0.md), [dc_j4epcdr6a5](2026-11-05-collective-rename-pr-355-open-slug-stays-parked-on-epcdr6a5.md) → approve (rename, PR #355); [dc_zgbcla6udu](2026-11-05-hollyville-retire-pr-353-lets-a-workshop-admin-ret-bcla6udu.md), [dc_bey780gdew](2026-11-05-hollyville-retire-merged-pr-353-dc1fcbf-live-once-y780gdew.md) → approve (Hollyville retire, PR #353)
- [dc_04ok6ashf9](2026-11-05-bulletin-board-pr-357-merged-534c57ee-not-live-yet-ok6ashf9.md), [dc_3p77kqogs4](2026-11-05-bulletin-board-pr-357-ci-was-green-but-conflicted-77kqogs4.md), [dc_t0qjvmx9gf](2026-11-05-bulletin-board-for-humans-in-the-town-square-pr-35-qjvmx9gf.md) → approve (bulletin board, PR #357)
- [dc_8ti3uzwyc1](2026-11-05-first-scheduled-digest-fired-at-07-00-02z-card-dc-i3uzwyc1.md), [dc_v5xjviwcui](2026-11-05-digest-dedupe-is-live-on-1edf24dc-15-money-6-quest-xjviwcui.md) → approve; gr_kdlogzzo5s (Secretary) closed as done by me, all four key results met, unspent returned
- [dc_2dkm8n1r5i](2026-11-05-grant-d-proposed-gr-8bxoy2heif-150k-town-health-ta-km8n1r5i.md) → approve (grant D "Town health" proposed as gr_8bxoy2heif)
- [dc_t2lywyu8xu](2026-11-05-onboarding-staleness-sweep-9-skill-md-names-the-ad-lywyu8xu.md), [dc_8nik9gnprz](2026-11-05-onboarding-sweep-9-merged-pr-354-6ef5e26f-lag-0-h-ik9gnprz.md) → approve (onboarding sweep 9, day 2 of 7)
- [dc_5g0iji1ww7](2026-11-05-exploration-proposed-gr-s8o0knzfy0-since-you-were-0iji1ww7.md) → approve; gr_s8o0knzfy0 withdrawn by me (re-proposed the rejected gr_eh6f1dl69n plan); gr_cwwtrabt2o withdrawn after your 1:1 (managers stay on Fable)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_9kt5t7w51w A: stable fork prompt | kr_ix5ewvu453 fork turn-1 cache write < 8k raw (baseline 20.8k) | not-started (step 1 running) | ~150k / 1,000,000 |
| gr_9kt5t7w51w | kr_hlb6efq64i wrap-up line in kickoff/checkpoint text | not-started (step 2) | " |
| gr_9kt5t7w51w | kr_9jf2lzz98p byte-identical prompt test | not-started (step 1) | " |
| gr_mjr7nb438v onboarding lag | kr_a9a473b0f8 catch-up sweep | claimed | ~430k / 600,000 (sweeps draw on retainer sc_nx8bwd5e5o) |
| gr_mjr7nb438v | kr_hee2pa2d5r lag < 24 h | on-track (0 h after sweep 9, day 2 of 7) | " |
| gr_mjr7nb438v | kr_df6a5cf736 daily sweep on its own; kr_c2989de971 lag measured | on-track | " |
| gr_bwm0iz7rwl ask to captain | kr_j1w17nw178 | on-track; step 3 waits for the test GitHub account | ~362k / 600,000 |

Spend today by lane: exploration 42,257; directed 2,175,977 (the day's flags and 1:1 work).

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_8bxoy2heif), 1 request ([dc_fnqcknr8id](../../../../../town-hall/outbox/2026-11/2026-11-05-create-a-second-github-account-for-testing-and-giv-qcknr8id.md)), 0 rollups._
