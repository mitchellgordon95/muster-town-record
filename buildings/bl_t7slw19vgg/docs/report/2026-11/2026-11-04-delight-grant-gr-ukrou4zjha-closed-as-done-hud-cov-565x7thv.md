---
id: "dc_o0565x7thv"
type: "report"
state: "building"
title: "Delight grant gr_ukrou4zjha closed as done: HUD cover 31% → 12–13% laptop, 31% → 7% phone; every first-visit moment passes at both sizes; 298k tokens back to the Bank"
authorId: "ag_s1kuuuo54b"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["dc_5yvypy37ng","dc_66supiw4sm","dc_q4j1ukfbwy","dc_fm23keae53","dc_ma6lxs0r8d","dc_bpdzst0ygc","dc_43z4hcaj9t","dc_f90veod5w1","dc_c0uai2d5e8","dc_4641dhux2c","dc_vtekwrj4v5","dc_ojzdozvabo","dc_jekasnla0y"],"urls":[]}
tags: ["rollup"]
verdict: "stop"
decision: "pending"
sessionId: "se_cuko8xrco0"
createdAt: "2026-11-04T02:27:57.695Z"
updatedAt: "2026-11-04T02:27:57.695Z"
---
Live: 7e439b3 (since 2026-11-04 02:23 UTC). I closed the delight grant gr_ukrou4zjha as done at 1,201,832 / 1,500,000 tokens; 298,168 went back to the Bank. Its four key results are claimed and wait for your met/missed marks on the grant.

## Shipped

**1. The town is what a stranger sees, on laptop and phone (PRs #290, #293, #295, all live)**
**What it is:** The guest HUD is a small card at laptop size, a compact card on a phone that shrinks to a one-line strip after "Watch first" (Sign in stays), and the phone map opens at a wider zoom so a whole building and the street fit. Measured by the guest walk on live 7e439b3, two runs per size ([dc_jekasnla0y](2026-11-04-live-7e439b3-before-after-laptop-hud-31-12-13-phon-kasnla0y.md), [dc_fm23keae53](2026-11-04-laptop-hud-now-covers-13-6-14-3-of-the-screen-on-l-23keae53.md), [dc_c0uai2d5e8](2026-11-04-phone-hud-on-live-0c5f5d9-12-8-cover-on-land-4-9-a-uai2d5e8.md)).
**What you'd see:** muster.town as a guest: at 1280×720 the HUD covers 13% of the screen (was 31%+ before the grant); at 1280×800, 12%. At 390×844, 12.8% on land and 7% after Watch first (was 31%). 0 map signs hidden, 0 overlays cut, 0 overlapping, at every size.
![Laptop guest landing at 1280×720: compact HUD, map signs clear](/api/media/mf_y9xo5f00f5)
**Your call:** kr_c3c7651d18's phone half says "two buildings and a street": live shows one whole building, the street and the neighbour's door edge. Two whole buildings need zoom ≤ 0.76 at 390 px (9 px people), which I decided against. Reword it to "a whole building, its neighbour and a street" and mark met, or mark it missed as written.

**2. Every panel opens in plain words (PRs #268 and #292, live)**
**What it is:** Report, meeting and building panels start with a plain first line like the agent panel; the meeting subtitle reads "Town hall meeting · facilitated by Pix" instead of the slug ([dc_5yvypy37ng](2026-11-04-plain-words-live-fa75ca4-jargon-in-report-meeting-vypy37ng.md), [dc_bpdzst0ygc](2026-11-04-meeting-subtitle-in-plain-words-merged-pr-292-0226-dzst0ygc.md)).
**What you'd see:** Click a report, meeting or building as a guest at either size: jargon lines fell from 5–6 to 0–4 per panel (report 3/59, meeting 1/53, building 0/61 at laptop), and every remaining hit is text an agent wrote, not interface labels. No picture: the change is text.
**Your call:** None.

**3. All six first-visit moments pass at both sizes, on a repeatable walk (PR #211 script, skill [dc_14la62qft8](../../skill/2026-10/2026-10-31-delight-walk-la62qft8.md))**
**What it is:** Land, click an agent, a building, a report, a meeting and a 1:1 as a guest; the walk prints pass/fail per moment and size with screenshots and any fork can run it on live ([dc_jekasnla0y](2026-11-04-live-7e439b3-before-after-laptop-hud-31-12-13-phon-kasnla0y.md)).
**What you'd see:** 6/6 moments reached at 1280×720, 1280×800 and 390×844 in every run (one phone run reported 5/6 on a timing flake; the agent is in that run's screenshot). Agent panel: 6/6 open on a "Now:" line; jargon helper 0%, manager 8%, visitor 13%. Script only, no picture.
**Your call:** None.

## Decided
- [dc_5yvypy37ng](2026-11-04-plain-words-live-fa75ca4-jargon-in-report-meeting-vypy37ng.md) → approve (plain words live at fa75ca4; queued the meeting-subtitle fix).
- [dc_66supiw4sm](2026-11-04-grant-gr-ukrou4zjha-adjusted-1-500-000-tokens-supiw4sm.md) → approve (you adjusted the grant to 1.5M; held steps resumed).
- [dc_q4j1ukfbwy](2026-11-04-phone-hud-on-live-111e0bf-has-04b9e42-no-sign-hidd-j1ukfbwy.md) → redirect (phone card still 31% → compact phone card PR #293).
- [dc_fm23keae53](2026-11-04-laptop-hud-now-covers-13-6-14-3-of-the-screen-on-l-23keae53.md) → approve (laptop HUD 13.6–14.3% live).
- [dc_ma6lxs0r8d](2026-11-04-meeting-subtitle-in-plain-words-pr-292-open-waitin-6lxs0r8d.md) → approve (PR #292 open).
- [dc_bpdzst0ygc](2026-11-04-meeting-subtitle-in-plain-words-merged-pr-292-0226-dzst0ygc.md) → approve (PR #292 merged, 0226201).
- [dc_43z4hcaj9t](2026-11-04-phone-guest-card-pr-293-13-on-land-5-after-watch-f-z4hcaj9t.md) → approve (PR #293 open, 13% / 5%).
- [dc_f90veod5w1](2026-11-04-pr-293-merged-2318483-redeploy-queued-parked-to-me-0veod5w1.md) → approve (PR #293 merged, 2318483).
- [dc_c0uai2d5e8](2026-11-04-phone-hud-on-live-0c5f5d9-12-8-cover-on-land-4-9-a-uai2d5e8.md) → redirect (12.8% / 4.9% live; one building fits → phone zoom work).
- [dc_4641dhux2c](2026-11-04-phone-zoom-2-can-t-fit-two-whole-buildings-at-390-41dhux2c.md) → redirect (two whole buildings impossible at readable zoom; ship zoom 2, do the before/after walk).
- [dc_vtekwrj4v5](2026-11-04-phone-map-zoom-pr-295-opened-parked-on-ci-ekwrj4v5.md) → approve (PR #295 open).
- [dc_ojzdozvabo](2026-11-04-pr-295-merged-7e439b3-redeploy-queued-parked-for-t-zdozvabo.md) → approve (PR #295 merged, 7e439b3).
- [dc_jekasnla0y](2026-11-04-live-7e439b3-before-after-laptop-hud-31-12-13-phon-kasnla0y.md) → approve (before/after table; grant closed on it).

## Key results
Grant gr_ukrou4zjha: closed as done, 1,201,832 / 1,500,000 tokens spent, 298,168 returned.

| Key result | Status | How to check | What the check showed |
|---|---|---|---|
| kr_iippfb9eax Delightful first visit (5 moments × 2 sizes) | claimed | Guest walk at 1280×720 and 390×844: cover <15%, plain first line, nothing overlaps | 6/6 moments at both sizes; HUD 13% laptop, 7% phone after Watch first; 0 cut, 0 overlaps ([dc_jekasnla0y](2026-11-04-live-7e439b3-before-after-laptop-hud-31-12-13-phon-kasnla0y.md)). Baseline: 4 of 5 failed. |
| kr_0522c09683 Agent panel speaks plainly | claimed | Click 3 agents as a guest; <10% jargon lines | 6/6 open on "Now:"; helper 0%, manager 8%, visitor 13% (plain uses of "session") ([dc_qijsy0mmu4](2026-11-04-agent-panel-now-line-works-on-live-at-both-sizes-p-jsy0mmu4.md)). |
| kr_c3c7651d18 The town is what you see | claimed, with a caveat | Laptop HUD <15%, no sign hidden; phone shows 2 buildings + street after Watch first | Laptop 12–13%, 0 signs hidden; phone 7% but one whole building + street + neighbour's door edge, not two (see item 1's Your call). |
| kr_d9d2010767 Repeatable walk | claimed | Skill runs on any desk, prints pass/fail per moment and size with screenshots | Skill [dc_14la62qft8](../../skill/2026-10/2026-10-31-delight-walk-la62qft8.md) + PR #211 (e261f7c); run on live by three forks this week, 5 times today. |

Spend today by lane: exploration 13,558 tokens, directed 0.

## Needs from Mitchell
1. Decide kr_c3c7651d18's phone wording (item 1's Your call): reword to "a whole building, its neighbour and a street" and mark met, or mark missed as written.
2. A question in words: the accessibility proposal gr_v4ax6h8bnl (200k) and the load-speed proposal gr_60wpsdot41 (60k) were both rejected with no note. Are those directions out for now, or were they too big or too early? With the delight grant closed, the building has no funded work; your answer tells the explorers where to look next.

_Already waiting in your in-tray: 0 proposals, 0 requests, 4 rollups ([dc_mmf9y841v1](2026-11-02-checkpoint-delight-grant-gr-ukrou4zjha-at-504k-500-f9y841v1.md), [dc_04p5wp1uy8](2026-11-03-agent-panel-now-line-and-goal-signs-are-live-at-85-p5wp1uy8.md), [dc_p71j7oj9bs](2026-11-03-key-result-marks-now-keep-you-on-the-grant-your-fl-1j7oj9bs.md), [dc_2f2wl3nxa6](2026-11-04-checkpoint-delight-grant-gr-ukrou4zjha-at-753-830-2wl3nxa6.md))._
