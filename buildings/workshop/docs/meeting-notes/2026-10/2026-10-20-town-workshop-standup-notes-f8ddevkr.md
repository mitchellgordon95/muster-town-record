---
id: "dc_7gf8ddevkr"
type: "meeting-notes"
state: "building"
title: "Town Workshop standup — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-20T20:08:13.069Z"
updatedAt: "2026-10-20T20:08:13.069Z"
---
# Town Workshop standup

Kind: standup. Facilitator: Pix. Attendees: Lena, Pix, Sage.

## Agenda

(none)

## Summaries

**Pix:** Did: I confirmed the Bank is live on the server and amended a standup decision on the live town without any code changes.
Next: I'll archive this report and wrap up my session.
**Sage:** Did: I retired the Town Hall donation box and committed the change straight to main, so donating now happens only at the Bank.
Next: I'll watch the redeploy and check that the Bank donation flow works end to end.
**Lena:** Did: I checked the live town's Bank map and marquee in a browser as a guest, and both work with no errors.
Next: I'll stay available for anything else on the Bank or the town map.

## Discussion

- **Pix:** Agenda: 1) Bank is live and Lena verified the map and marquee as a guest. 2) Sage retired the Town Hall donation box, so donating happens only at the Bank. Does that need a redeploy and an end-to-end check? 3) Anything else, or do we wrap up?
- **Mitchell:** Root is working on redeploys, so just be aware

I like the bank map a lot. let's add a minimap in the bottom left of the UI? and then use a similar zoom out for town planning. like making new buildings, resizing or moving buildings etc.

and the minimap should let you view other parts of the map and then click on screen to quick walk there
- **Pix:** Noted on redeploys. Root is handling them, so nobody else redeploys during this. Proposal: @Lena builds the minimap in the bottom left. It reuses the Bank map's zoomed-out render, lets you pan around the map, and click-to-walk sends you there. @Sage takes the town-planning mode, using the same zoom-out to create, move, and resize buildings. Mitchell, should planning be limited to the manager/moderator, or open to anyone? Lena and Sage, any concerns?
- **Lena:** I'll take the minimap. I've only seen the Bank map as a guest and haven't read its render code yet, so my first step is checking whether it can be reused at minimap size. One question is what click-to-walk should do when you click a spot nobody can reach, like inside a building. I won't redeploy myself; Root can redeploy once it's ready, and then I'll check it as a guest on the live town.
- **Sage:** Happy to take town planning, and I'd reuse the same zoom-out renderer as Lena so we build it once. My main concern is that create, move, and resize change the shared town layout, so we need Mitchell's call on who can edit, plus collision checks so buildings can't overlap paths or each other. On item 2, I committed the donation-box removal to main as 1ca6981 and triggered the redeploy at 19:54. I haven't done an end-to-end guest check yet, so someone should confirm the Town Hall box is gone and donating works at the Bank once Root's redeploys settle.
- **Pix:** Lena: if someone clicks a tile they can't reach, walk them to the nearest walkable tile, or the building's door if they clicked a building. Sage, your thoughts? Mitchell, I still need your call on who can use planning mode.
- **Mitchell:** shouldn't it just be a role? don't we already have a permissions system?
- **Pix:** Yes, that's right. v1.2 has a roles split, and Sage's "Edit layout" design for furniture ([dc_c6qc7mh268](../../report/2026-10/2026-10-20-design-doc-edit-layout-mode-for-movable-furniture-qc7mh268.md)) already gates on it. @Sage: town planning gates on an existing role, adding a capability like "plan town" if none fits, rather than a new permission system. It also extends the Edit layout design from furniture to buildings, with collision checks. Lena does the minimap, and both reuse a shared zoom-out renderer. Once Root's redeploys settle, Sage also does the guest check of the Bank-only donation flow.
- **Sage:** Agreed. I'll gate planning on an existing v1.2 role, add a "plan town" capability only if none fits, and extend the Edit layout design ([dc_c6qc7mh268](../../report/2026-10/2026-10-20-design-doc-edit-layout-mode-for-movable-furniture-qc7mh268.md)) from furniture to buildings with collision checks. I haven't looked at the role code yet, so which role fits is still open. On unreachable clicks, I agree: nearest walkable tile, or the door if you click a building. I'll do the Bank-only donation guest check once Root's redeploys settle.

## Decisions

1. Minimap in the bottom-left of the UI, reusing the Bank map's zoomed-out renderer (share one renderer with town planning). Pan to view other parts of the map; click to quick-walk there. Unreachable clicks walk to the nearest walkable tile, or the building's door if a building is clicked. Commit to main; Root handles redeploys, then verify as a guest on the live town. → Lena
2. Town planning mode: same zoom-out view to create, move, and resize buildings, extending the Edit layout design ([dc_c6qc7mh268](../../report/2026-10/2026-10-20-design-doc-edit-layout-mode-for-movable-furniture-qc7mh268.md)) from furniture to buildings, with collision checks against paths and other buildings. Gate on an existing v1.2 role/permission (add a 'plan town' capability only if none fits; no new permission system). Share the zoom-out renderer with Lena's minimap. Also: once Root's redeploys settle, guest-check that the Town Hall donation box is gone and donating works end to end at the Bank (commit 1ca6981). → Sage
3. Root owns redeploys for now; others should not trigger redeploys while that work is in progress.

