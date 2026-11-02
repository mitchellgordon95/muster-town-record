---
id: "dc_5mxhq4gy9l"
type: "report"
state: "building"
title: "UI / UX rollup: fountain town polish is live, and an accessibility baseline with a grant proposal"
authorId: "ag_s1kuuuo54b"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["dc_ud72lk6pfy","dc_p6zduycubl","dc_8aitzef4qj","dc_j8yjsnvamu","dc_9asrc6iywm","dc_sqogyxgy2a"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-11-01T01:38:04.471Z"
sessionId: "se_tlbbpiepnx"
createdAt: "2026-11-01T01:22:09.440Z"
updatedAt: "2026-11-01T01:38:04.471Z"
---
Live: 7521c0b. Our fountain polish (8c8389c) has been live since f729e03.

## Shipped
**1. The fountain town now has doors on any side, and nothing overlaps on it**
**What it is:** The live map uses the "fountain" shape, a town round a square. Each building's door faces its avenue. The Bank's gold token sign now scales to fit its own lawn, so it no longer runs over UI/UX. In town planning on a phone, the shape toolbar now sits at the bottom of the screen instead of on top of the HUD. Details: PR #205 and PR #220 (8c8389c), reports [dc_8aitzef4qj](../2026-10/2026-10-31-fountain-town-and-doors-on-any-side-verified-live-itzef4qj.md) and [dc_p6zduycubl](../2026-10/2026-10-31-fountain-polish-verified-live-8c8389c-in-f729e03-b-zduycubl.md).
**What you'd see:** Open muster.town at laptop size. The Bank's marquee stops about one tile short of the UI/UX wall at both zoom 2 and zoom 3. On a phone, open town planning: the toolbar is at the bottom with about 360 px of clear map above it. The live layout matches the code tile for tile (113×37 tiles, 7 lots). The screenshots are on the desk only; none were uploaded.
**Your call:** None.

**2. Accessibility baseline (findings only, no code changed)**
**What it is:** A check of the live town for guests who use a keyboard or a screen reader ([dc_ud72lk6pfy](2026-11-01-exploration-accessibility-baseline-automated-check-72lk6pfy.md), findings [dc_j30iosk7ys](../../note/2026-11/2026-11-01-findings-can-a-stranger-who-uses-a-keyboard-or-a-s-0iosk7ys.md)).
**What you'd see:**
- axe finds only one failure: the 3 welcome-card links have 2.07:1 contrast against the 4.5:1 required.
- The map canvas has no label, and the page has 0 live regions and 0 landmarks.
- Enter on an agent row in "Who is here now" walks you to the agent but doesn't open its panel.
- Focus doesn't move into a panel when it opens.

This led to grant proposal gr_v4ax6h8bnl.
**Your call:** None beyond the proposal.

## Decided
- [dc_ud72lk6pfy](2026-11-01-exploration-accessibility-baseline-automated-check-72lk6pfy.md) → approve (accessibility baseline; grant proposed)
- [dc_p6zduycubl](../2026-10/2026-10-31-fountain-polish-verified-live-8c8389c-in-f729e03-b-zduycubl.md) → approve (fountain polish verified live)
- [dc_8aitzef4qj](../2026-10/2026-10-31-fountain-town-and-doors-on-any-side-verified-live-itzef4qj.md) → approve (fountain town verified live)
- [dc_j8yjsnvamu](../2026-10/2026-10-31-fountain-polish-bank-sign-fits-its-lawn-at-any-zoo-yjsnvamu.md) → approve (PR #220)
- [dc_9asrc6iywm](../2026-10/2026-10-31-pr-220-merged-8c8389c-redeploy-queued-parked-to-ve-src6iywm.md) → approve (PR #220 merged, redeploy)
- [dc_sqogyxgy2a](../2026-10/2026-10-31-phone-and-laptop-goal-signs-stay-on-screen-and-off-ogyxgy2a.md) → approve (PR #219: goal signs stay off the HUD; its merge is held with the grant at checkpoint)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_ukrou4zjha | kr_iippfb9eax Delightful first visit | not-started | 351,181 / 250,000 (at checkpoint) |
| gr_ukrou4zjha | kr_0522c09683 Agent panel speaks plainly | not-started | same grant |
| gr_ukrou4zjha | kr_c3c7651d18 The town is what you see | not-started | same grant |
| gr_ukrou4zjha | kr_d9d2010767 Repeatable walk | not-started | same grant |

Today's spend: exploration 35,575 tokens (free under the goal: 9,126,098); directed 0 tokens. Five queued assignments are held while gr_ukrou4zjha sits at its checkpoint, including the merges of PR #219, #217 and #211.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_v4ax6h8bnl), 0 requests, 0 rollups._
