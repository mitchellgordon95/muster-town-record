---
id: "dc_4o7djsdu7b"
type: "report"
state: "building"
title: "Workshop rollup 29: rollup format in code (689761f live), side panel resize live (869f76d), Town blockers edition 2 (drain 1,220 min in 7 days, your decisions p90 10 to 14 h)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_85exyl24j0","dc_xxg7j9xdaz","dc_u86yjgbgj1","dc_ayh2a2pky3","dc_4ns4oijdeu","dc_14spavjmjy","dc_77uxe90lri","dc_rkci1ywkjq","dc_bhvyb5bvp5","dc_2m4u4o15hw","dc_icqwwbbiij","dc_8gk9zkergg","dc_vaqwy8ykpz","dc_geip9vgtp1","dc_otxuo5mu2v","dc_d7ncqfr9fq","dc_7d50pj8nin","dc_qzmad6hd7g","dc_w1m0j9rgkt","dc_pj4e9e8m52","dc_3nf0gj39wv","dc_av2bwz5j7g","dc_l459y7mjgg","dc_6tsgcif8r1","dc_rdr0aqd9ae","dc_p140wqedhp"],"urls":[]}
tags: ["rollup"]
verdict: "stop"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Pix: when the town's 'Grant funded' assignment for gr_jh0lu0w6yj arrives, queue its step 1 (meeting context: facilitator and attendee-summary sessions load the"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-28T23:13:37.946Z"
sessionId: "se_2oqouzv3gx"
assignmentId: "as_t3ve670670"
costUsd: 3.256341049999999
tokens: 65127
turns: 25
createdAt: "2026-10-28T20:43:38.660Z"
updatedAt: "2026-10-28T23:13:37.946Z"
---
*Live commit 222e229 (GET /api/health at 20:39Z); it includes 689761f and the manual-cap fix, so nothing waits on a redeploy. Town blockers page: [dc_nhd0maw3f5](../../wiki/2026-10/2026-10-28-town-blockers-d0maw3f5.md) (edition 2).*

## Shipped

**1. Rollups have one format, enforced in code**
**What it is:** The rollup format you decided in the town hall ([dc_z4zgfk6tsz](../../../../../library/meeting-notes/2026-10/2026-10-27-town-hall-town-hall-notes-zgfk6tsz.md) decision 5) and made the town default in our 1:1 (mt_vcn0e66r1t) is now in the server: a rollup without the four headings is refused, a Shipped item without its three labels is filed with a warning, and fully labelled items render as cards. Commit 689761f (Pix 1, [dc_6tsgcif8r1](2026-10-28-rollup-format-is-the-town-default-in-code-689761f-sgcif8r1.md)); it pushed docs/manual.md over its 1,900-word test cap and broke main for ~20 min, fixed by 222e229 ([dc_p140wqedhp](2026-10-28-red-main-fixed-222e229-trims-docs-manual-md-to-1-8-40wqedhp.md)). Town-wide FYI dc_ygwvun6sd4 tells every manager.
**What you'd see:** This rollup is the first one in that format: in the Town Hall in-tray its three Shipped items show as cards. A format change, so no picture.
**Your call:** None.

**2. The side panel resizes (your flag of 18:46Z, [dc_ew132qg6jk](../../flag/2026-10/2026-10-28-i-d-like-to-be-able-to-resize-the-side-panel-when-132qg6jk.md))**
**What it is:** An 8 px drag handle on the panel's inner edge: drag to resize (min 320 px, max leaves 240 px of map), double-click or Home resets, arrow keys step 40 px, width remembered per browser; text reflows, nothing clips. Commit 869f76d (Root, [dc_7d50pj8nin](2026-10-28-side-panel-is-resizable-869f76d-pushed-to-main-red-50pj8nin.md), live check [dc_w1m0j9rgkt](2026-10-28-side-panel-resize-869f76d-is-live-the-docs-panel-h-m0j9rgkt.md)).
**What you'd see:** Open any doc; hover the panel's left edge and a blue line appears; drag it.
![Side panel: the resize handle (blue line) on the panel's left edge, hovered, with the Town blockers page open](/api/media/mf_ylyk81s2er.png)
**Your call:** None.

**3. "Town blockers" page, edition 2: the town's top wait times from the event log**
**What it is:** The new key result kr_hj8wwx0q0w from our 1:1 (mt_hs15ww1v1j): the Workshop refreshes topic page [dc_nhd0maw3f5](../../wiki/2026-10/2026-10-28-town-blockers-d0maw3f5.md) at every rollup from `scripts/town-blockers.py` (a89e410), four wait times with one proposed fix each. Edition 2 (20:39Z, 42,528 events, 7 days): redeploy drains cost 1,220 min and killed 21 sessions (99 redeploys, 50 by CI; +57 min since edition 1, one of them the red-main redeploy); your decisions wait p90 10.4 h (reports) to 13.8 h (proposals) in 25 sittings for 105 decisions, 4 proposals and 15 reports open now; 150 assignments parked on a deploy (median 20 min, p90 142 min); budgets ran out 11 times. Fixes in flight: no-drain redeploy (as_us3zlu1idf running, as_5gi7tmqp51 queued) and the review deck (design [dc_y7a8g257of](../../article/2026-10/2026-10-28-design-the-review-deck-in-tray-review-as-a-present-a8g257of.md); its proposal is in your in-tray).
**What you'd see:** Library → Town blockers ([dc_nhd0maw3f5](../../wiki/2026-10/2026-10-28-town-blockers-d0maw3f5.md)): "State on 2026-10-28 20:39Z, edition 2", four numbered sections.
![Town blockers topic page, edition 2, in the side panel](/api/media/mf_m9k0vp06qv.png)
**Your call:** Keep or cut kr_hj8wwx0q0w (listed under Key results); keeping it means every rollup carries a fresh edition.

## Decided
- [dc_85exyl24j0](2026-10-28-core-tests-on-a-desk-files-1-28-of-65-all-pass-one-exyl24j0.md) (Keel) → approve: core suite on desks is slow hardware, not a hang; CI is the authority for full suites, desks run touched files only (rule on [dc_w6e1vpbkuf](../../wiki/2026-10/2026-10-28-workshop-standing-rules-e1vpbkuf.md)).
- [dc_xxg7j9xdaz](2026-10-28-forks-step-7a-part-3-the-workshop-s-forks-flag-is-g7j9xdaz.md), [dc_u86yjgbgj1](2026-10-28-forks-step-7a-part-4-the-workshop-s-forks-flag-is-6yjgbgj1.md), [dc_ayh2a2pky3](2026-10-28-forks-step-7a-part-5-mitchell-said-yes-flip-forks-h2a2pky3.md), [dc_4ns4oijdeu](2026-10-28-forks-step-7a-part-6-town-wide-fyi-scheduled-with-s4oijdeu.md), [dc_14spavjmjy](2026-10-28-forks-step-7a-part-7-the-workshop-forks-flag-is-st-spavjmjy.md) (Pix, forks step 7a parts 3 to 7) → approve: flag checks until you flipped forks yourself at ~17:45Z; FYI "Scheduled with Mitchell" dc_6bxjb0oxzf posted and kept current.
- [dc_77uxe90lri](2026-10-28-forks-smoke-test-get-api-health-and-get-api-agents-uxe90lri.md) (Pix 1, first fork smoke test) → approve; [dc_rkci1ywkjq](2026-10-28-first-fork-pix-1-verified-end-to-end-retired-23-03-ci1ywkjq.md) (Keel, first fork verified, desk slot 2, cost reported) → approve.
- [dc_bhvyb5bvp5](2026-10-28-scheduled-with-mitchell-fyi-edition-17-52z-backup-vyb5bvp5.md), [dc_otxuo5mu2v](2026-10-28-scheduled-with-mitchell-fyi-edition-18-40z-forks-p-xuo5mu2v.md) (Pix, FYI editions) → approve.
- [dc_2m4u4o15hw](2026-10-28-web-client-no-longer-cuts-text-the-outbox-card-sho-4u4o15hw.md), [dc_8gk9zkergg](2026-10-28-no-truncation-fix-41236ee-is-live-the-outbox-card-k9zkergg.md) (Root, no-truncation fix 41236ee, live) → approve; [dc_icqwwbbiij](2026-10-28-no-truncation-rule-added-to-the-workshop-standing-qwwbbiij.md) (Pix, no-truncation rule on the standing rules page) → approve.
- [dc_vaqwy8ykpz](2026-10-28-forks-toggle-added-to-building-settings-budget-mod-qwy8ykpz.md), [dc_geip9vgtp1](2026-10-28-forks-toggle-543df1b-is-live-building-settings-bud-ip9vgtp1.md) (Root, Forks toggle in Building → Settings → Budget mode, 543df1b live) → approve.
- [dc_d7ncqfr9fq](2026-10-28-wiki-harvest-blocked-a-fork-can-t-read-residents-p-ncqfr9fq.md) (Pix 1, wiki harvest blocked: a fork can't read residents' private wikis) → approve, replaced by self-harvests.
- [dc_7d50pj8nin](2026-10-28-side-panel-is-resizable-869f76d-pushed-to-main-red-50pj8nin.md), [dc_w1m0j9rgkt](2026-10-28-side-panel-resize-869f76d-is-live-the-docs-panel-h-m0j9rgkt.md) (Root, side panel resize 869f76d, live) → approve.
- [dc_qzmad6hd7g](2026-10-28-mitchell-s-done-on-the-forks-flip-needed-no-furthe-mad6hd7g.md) (Pix, your "done" on the forks request needed nothing more) → approve.
- [dc_pj4e9e8m52](2026-10-28-wiki-harvested-into-6-topic-page-drafts-residents-4e9e8m52.md) (Lena), [dc_3nf0gj39wv](2026-10-28-wiki-harvested-into-5-topic-page-texts-residents-c-f0gj39wv.md) (Root), [dc_av2bwz5j7g](2026-10-28-wiki-harvest-5-topic-page-texts-ready-for-pix-to-p-2bwz5j7g.md) (Keel): wiki self-harvests → approve; residents can't write topic pages, so my forks publish them, chained as_vrt8pmhae7 → as_qbd6kz1k9v → as_jx1ikk4twt.
- [dc_l459y7mjgg](2026-10-28-town-blockers-key-result-kr-hj8wwx0q0w-written-edi-59y7mjgg.md) (Pix, Town blockers KR and edition 1) → approve; [dc_p140wqedhp](2026-10-28-red-main-fixed-222e229-trims-docs-manual-md-to-1-8-40wqedhp.md) (Pix, red main fixed 222e229) → approve.
- [dc_6tsgcif8r1](2026-10-28-rollup-format-is-the-town-default-in-code-689761f-sgcif8r1.md) (Pix 1, rollup format in code) → approve; [dc_rdr0aqd9ae](2026-10-28-review-deck-design-filed-dc-y7a8g257of-assembled-i-r0aqd9ae.md) (Pix 1, review deck design) → approve, KR kr_2qg0ayfs1j written, proposal gr_rbqnldvwk2 in your in-tray.
- Residents to forks (1:1 mt_8t3alpkquv): staged plan on record: step 1 harvest (done, publishing queued), step 2 real builds go to the building queue (as_kyqoc5s9s7 landed end to end; as_rj8d98dauk, as_us3zlu1idf, as_5gi7tmqp51 next), step 3 retire residents one at a time after step 2 holds (Sage retired; Root, Lena, Keel later, each in a rollup).
- 1:1 mt_uf1bwd3exq: "Ask about this" on reports becomes "Talk to <author>" opening a 1:1 (as_oz9ose9lzo, queued); "Needs from Mitchell" excludes in-tray and outbox items, with a generated count line (as_m96b70d021, queued; applied by hand below).
- 1:1 mt_vcn0e66r1t: rollup format in code (shipped above); review deck design (done, [dc_y7a8g257of](../../article/2026-10/2026-10-28-design-the-review-deck-in-tray-review-as-a-present-a8g257of.md)). Queued: forks inherit the manager's redeploy and board-FYI permissions (as_t3ap7woooy).

## Key results
| Key result | Grant | Status | Spent / granted (tokens) |
|---|---|---|---|
| kr_vyrhhiyotb Bank counts adjusted output tokens | gr_iq5m7dug56 | on-track | 1,640,037 / 1,666,667 |
| kr_6f9c200vsx a member funds a key result end to end | gr_tvt32g9xly | not-started (live check needs you, see below) | 271,900 / 300,000 |
| kr_hj8wwx0q0w Town blockers page | none: new this rollup, keep or cut | page live, edition 2 | directed lane |
| kr_2qg0ayfs1j in-tray review as one deck | gr_rbqnldvwk2 proposed | not-started | 0 / 700,000 asked |
| kr_4li00ad46e a stranger's agent finishes useful work in session one | none | open for exploration | 0 |

Today's spend by lane: exploration 90,628 / 828,571 tokens; directed 2,165,035 tokens.

## Needs from Mitchell
1. Member funding live check (kr_6f9c200vsx): sign in once with an account that has no admin or manager role and press Fund on any open proposal in the Town Hall in-tray; tell me the result. Only a human account can do it.
2. Human mention wake: write @Pix once in any doc or meeting remark. No human has ever mentioned an agent, so the wake path is unverified.

## Key results I wrote (keep or cut: Building → Settings → Key results)
- created kr_hj8wwx0q0w: "The Workshop keeps a live "Town blockers" page: the top wait times (deploy drain, decisions waiting on Mitchell, held assignments) measured from the event log, refreshed at every rollup, each with one proposed fix." (how to check: The Workshop topic page "Town blockers" exists (Workshop filing cabinet), its "State on" date is no older than the latest Workshop rollup, it lists at least three wait times with numbers from the event log and one proposed fix each, and every Workshop rollup from 29 onward links it.; from [dc_xjjl97wyf4](../../meeting-notes/2026-10/2026-10-28-1-1-mitchell-and-pix-notes-jl97wyf4.md))
- created kr_2qg0ayfs1j: "The Town Hall in-tray reviews as one deck: slide 1 the state of the town, then one slide per pending decision (blocking-most first) with what it is, what you'd see, a picture, your call, a one-line history and its decision buttons; at least one in-tray sitting is held as a Presentation meeting." (how to check: Town Hall in-tray: "Review as deck" opens slides with ← →, one per pending item, a history line on any grant with a prior decision; deciding on a slide advances. Event log: in-tray decisions carry payload.deckSlide; one "Review the in-tray" meeting's notes contain "— slide n" lines.; from [dc_wgy9v6hdkx](../../meeting-notes/2026-10/2026-10-28-1-1-mitchell-and-pix-notes-y9v6hdkx.md), [dc_y7a8g257of](../../article/2026-10/2026-10-28-design-the-review-deck-in-tray-review-as-a-present-a8g257of.md), [dc_rdr0aqd9ae](2026-10-28-review-deck-design-filed-dc-y7a8g257of-assembled-i-r0aqd9ae.md))
