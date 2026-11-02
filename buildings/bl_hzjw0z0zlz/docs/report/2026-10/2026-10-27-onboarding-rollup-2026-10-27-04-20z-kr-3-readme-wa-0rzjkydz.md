---
id: "dc_cx0rzjkydz"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-27 04:20Z: KR 3 (README walk) cut and closed out, new key result kr_7316be4jqw (a signed-in stranger starts a collective at muster.town/<name> from the web) with grant gr_rdyrjzclfe proposed; operating manual still building; Mitchell: decide the grant, delete kr_tzg9en02dh"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_x93qiascyw","dc_ks5la608go"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Onboarding: gr_rdyrjzclfe (hosted collectives at muster.town/<name>, 1,000,000 adjusted tokens) is funded by Mitchell. Terms: anyone signed in may start a colle"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T17:43:04.337Z"
sessionId: "se_v7d1258dhs"
createdAt: "2026-10-27T04:04:01.811Z"
updatedAt: "2026-10-27T17:43:04.337Z"
---
## Shipped
Nothing new live since the last rollup ([dc_5t90uf7brx](2026-10-27-onboarding-rollup-2026-10-27-03-10z-operating-manu-90uf7brx.md), 03:10Z). In flight: Craig's operating manual (as_4y6ifkyyy5, directed, Town Hall document opened from the HUD "?"), then Tae's live check of it (as_cwj6zalrl5, queued behind Craig's).

## Decided
- [dc_x93qiascyw](2026-10-27-grant-gr-ibccoje227-cut-3qiascyw.md) (Town: gr_ibccoje227 cut at its checkpoint, 289,904 / 266,667 adjusted tokens, now closed) → approve. The work it called for was already done in as_hsg160mt74.
- [dc_ks5la608go](2026-10-27-kr-3-readme-walk-closed-out-tae-s-held-walk-cancel-5la608go.md) (Kelly: KR 3 close-out) → approve. Tae's held walk continuation as_sq6dx2fozp cancelled; the README "Run it" text (497a43b) stays live and correct for anyone who does want to self-host. New key result kr_7316be4jqw written from Town Hall decision 4 (notes [dc_z4zgfk6tsz](../../../../../library/meeting-notes/2026-10/2026-10-27-town-hall-town-hall-notes-zgfk6tsz.md)): a signed-in stranger starts their own collective from the web at muster.town/<name>, is its admin within 5 minutes, it is listed on the homepage, the Workshop at /workshop untouched. Grant gr_rdyrjzclfe proposed for it: 1,000,000 adjusted tokens, four PRs (hub: many collectives in one process under /<slug>/; one sign-in at the root; Start a collective form + POST /api/collectives, one per GitHub user, never spends the host's Claude token; live check with a second GitHub account + manual section). Out of scope: desks and funding for hosted collectives' agents (next key result), custom domains.

## Key results
No funded grant in the building right now.
- kr_z0mj5teeu7 (stranger path) on-track, no grant (gr_cm3zha6mk6 cut 2026-10-26).
- kr_1rpq0738sw (first minute) on-track, no grant (gr_vfyih8s6ri closed at checkpoint).
- kr_tzg9en02dh (README walk) still shows on-track but Mitchell cut it; needs deleting.
- kr_pxisdsocdp (read-only until Let in) not-started, build live and verified 5/5; waiting on Mitchell's real round trip with a never-granted GitHub account.
- kr_7316be4jqw (hosted collectives) not-started, proposal gr_rdyrjzclfe open.
Spend today: exploration 46,367 / 828,571 tokens; directed 93,041 tokens (manual build + KR 3 close-out).

## Needs from Mitchell
1. Fund, counter or reject gr_rdyrjzclfe in the Town Hall in-tray. One open point to settle with it: may anyone signed in start a collective (my default), or only people you have Let in first?
2. Delete kr_tzg9en02dh from the Onboarding goal (only a human can).

## Key results I wrote (keep or cut: Building → Settings → Key results)
- created kr_7316be4jqw: "A signed-in stranger starts their own collective from the web at muster.town/<name>: no clone, no server of their own. Within 5 minutes of clicking Start a collective they are its admin at muster.town/<name>/, it is listed on the homepage, and the Workshop at /workshop is untouched." (how to check: Private window on muster.town, GitHub account never granted a role: Start a collective (name, goal) lands on muster.town/<name>/ showing that name and goal; GET /<name>/api/me says admin; planning desk New building works; / lists the new tile; /workshop/ unchanged; under 5 min, nothing installed.; from [dc_z4zgfk6tsz](../../../../../library/meeting-notes/2026-10/2026-10-27-town-hall-town-hall-notes-zgfk6tsz.md))
