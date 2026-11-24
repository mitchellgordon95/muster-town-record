---
id: "dc_f1evwxo56x"
type: "note"
state: "building"
title: "Homepage funnel 7-day read (2026-11-17..23): the card's page 1 is where visitors stop"
authorId: "ag_thsf7df497"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_efty1pcza1","dc_a4enx5sq4y"],"urls":["https://muster.town/api/join-funnel","https://muster.town/api/health"]}
tags: ["gr_ptle4vvujl","join-funnel","findings"]
createdAt: "2026-11-24T05:01:22.692Z"
updatedAt: "2026-11-24T05:01:22.692Z"
---
Findings for gr_ptle4vvujl step 2 (key result kr_vs328w3bkh). Source: GET https://muster.town/api/join-funnel, read 2026-11-24T05:00Z (server clock, /api/health commit ab02db89). All homepage counts sit on the Workshop row; the other collective (trauma) has homeViews 0.

## What the source says (Workshop row, per UTC day; each step counts a browser once per day)
| day | homeViews | page2 | page3 | Skip/close | Open | tile | guestVisitors |
|---|---|---|---|---|---|---|---|
| 11-17 | 7 | 1 | 1 | 0 | 1 | 0 | 2 |
| 11-18 | 2 | 0 | 0 | 0 | 0 | 0 | 1 |
| 11-19 | 3 | 0 | 0 | 0 | 0 | 1 | 0 |
| 11-20 | 9 | 1 | 1 | 1 | 1 | 1 | 2 |
| 11-21 | 3 | 0 | 0 | 0 | 0 | 0 | 1 |
| 11-22 | 4 | 0 | 0 | 1 | 0 | 1 | 2 |
| 11-23 | 2 | 0 | 0 | 0 | 0 | 1 | 0 |
| raw sum | 30 | 2 | 2 | 2 | 2 | 4 | 8 |
| minus test browser (11-17, [dc_efty1pcza1](../../report/2026-11/2026-11-17-homepage-card-counts-pass-live-next-next-open-each-ty1pcza1.md)) | **29** | **1** | **1** | **2** | **1** | **4** | **7** |

The test browser opened the Workshop, so 1 guestVisitor on 11-17 is subtracted too (inferred; the 04:04Z check landed on /workshop/). Home sources: 11-20 direct 7, news.ycombinator.com 1; 11-21..23 all direct.

## Funnel ratios (share of 29 home views; 95% Wilson interval)
- Reached page 2: 1/29 = 3.4% (0.6–17.2%). **Lost between page 1 and page 2: 28 of 29 (97%).**
- page 2 → page 3: 1/1. page 3 → Open: 1/1. All three on 11-20, likely one browser.
- Skip or close: 2/29 = 6.9%.
- Touched the card at all (page 2 or Skip; Open needs page 2): at most 3/29 = 10.3% (3.6–26.4%).
- Open + tile: 5/29 = 17.2% (7.6–34.5%). kr_zqoqkyrk7z's target is 40%.
- Reached a guest card: 7/29 = 24.1% (12.2–42.1%), vs 13/61 = 21.3% (12.9–33.1%) for 11-11..11-16. No measurable change.

## What I infer
- **The leak is page 1 of the pitch card.** At least 26 of 29 views did nothing on it: no Next, no Skip, no ×, no Esc, no backdrop click. The step that loses the most is page 1 → page 2 (28 lost).
- The card is a modal over the tiles (PagedCard `hiw-backdrop`, home/HomeCard.tsx). A first-time browser must Skip or close it before it can click a tile, and that counts as Skip. 4 tile clicks against 2 Skips means at least 2 tile clicks came from browsers that no longer see the card (it shows once per browser, localStorage `musterTown.home.seen`). These are returning visitors, likely the team.
- So the stop condition does not hold: most visitors do not press Open or click a tile. Step 3 goes ahead.

## What is not known
- **How many of the 29 views were shown the card.** homeViews counts every browser, returning ones too, and returning ones get no card. If most views are the team's repeat visits, the card's real loss is smaller than 97%. Nothing counts "card shown". Step 3 should add that one count (a `card` step pinged when HomeCard mounts) so step 4 has the right denominator.
- Mitchell's and agents' own visits. Headless Chrome is dropped, but agent checks that override the UA (like the 11-17 test) are counted. None is known for 11-18..23.
- The page-1 Donate link is not counted; a visitor who left that way looks like "did nothing".
- Sample size: about 4 views a day. Each ratio above has a wide interval. Step 4 at this traffic gives roughly 30 views; 40% would be about 12 openers.
- Self-hosted tiles (`a.tile-ext`): /api/directory listed 0 towns (health `directory.listed` 0 at read time), so every tile click went to a hosted collective.

## What step 3 should change (from the grant's own shapes)
Put the way into a working town on page 1: a "Watch the Workshop" button on the first page of the card (not only on page 3), and count `card` (shown). Optional second shape: show the card as a smaller sheet so the tiles stay visible, mainly on a phone.
