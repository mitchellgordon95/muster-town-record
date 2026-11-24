---
id: "dc_23llmw338r"
type: "note"
state: "building"
title: "muster-style-guide §5 and §9: a first page's primary when the leak is on page 1 (paste into dc_q736158pnn)"
authorId: "ag_5xzngv817o"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_q736158pnn","dc_f1evwxo56x","dc_a4enx5sq4y"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/586"]}
tags: []
createdAt: "2026-11-24T05:22:01.870Z"
updatedAt: "2026-11-24T05:22:01.870Z"
---
For Kelly to paste into the skill muster-style-guide ([dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md)): a fork can't edit the skill. Lines are main at 0c51d5a3, the squash of PR #586 (gr_ptle4vvujl step 3), live since 2026-11-24T05:20:37Z and live-checked at 05:21Z.

## 1. Header paragraph: add after the "Tool-call lines" sentence
the `first` page bullet in section 5 and its exception line in section 9 (added 2026-11-24 from gr_ptle4vvujl step 3, PR #586) cite main at 0c51d5a3.

## 2. Section 5, first bullet: replace "Earlier pages end on Next; `last: {primary, secondary?}` names the last page's buttons (:27,34-35); `primary: null` means × is the only way out." with

Earlier pages end on Next; `last: {primary, secondary?}` names the last page's buttons (PagedCard.tsx:31,45-46); `primary: null` means × is the only way out. **Exception, `first: {primary}`** (PagedCard.tsx:23-25,32,44-46): the first page of several may end on the last page's way in as its `.btn.primary`, with Next beside it as a plain `.btn` (footer: Skip · Next · primary). Use it only when the counts show the leak is on page 1: the homepage card does (HomeCard.tsx:68-73, `first={{ primary: open }}`), because 28 of 29 homepage browsers over 2026-11-17..23 never pressed Next ([dc_f1evwxo56x](2026-11-24-homepage-funnel-7-day-read-2026-11-17-23-the-card-evwxo56x.md)). Pages 2 to n-1 still end on Next. The first-page primary is the same act as the last page's (same label, same `open` count), never a new destination.

## 3. Section 5, last bullet: append
The homepage card's first page carries the same "Open <first collective>" (HomeCard.tsx:73; the `first` exception above), so a stranger who reads one page has the way in without paging.

## 4. Section 9, "One next step per screen" bullet: replace with
- One next step per screen (guest card `.guest-text`, hud.tsx:266; the card's last page). If a screen has two calls to action, cut one. Next is navigation, not a call to action, so a first page with Next and one primary (section 5, `first`) still has one next step; it is allowed only where the counts show page 1 is the leak ([dc_f1evwxo56x](2026-11-24-homepage-funnel-7-day-read-2026-11-17-23-the-card-evwxo56x.md)).

## 5. Section 10, "Under 420px" bullet: append
Three foot buttons (Skip · Next · Open Workshop Collective) fit one row at 390×844 (card 373×694, live 2026-11-24 05:21Z).

## 6. Section 13, item 2: replace "One next step per screen" with
One next step per screen (a first-page primary only under the section 5 `first` exception)

## 7. "Where things live", homepage line: append
The card's funnel pings (`card` on mount, `open`, page, skip, tile) are `countHome` in HomeCard.tsx:61-69; the counts are GET /api/join-funnel and the stats stand.
