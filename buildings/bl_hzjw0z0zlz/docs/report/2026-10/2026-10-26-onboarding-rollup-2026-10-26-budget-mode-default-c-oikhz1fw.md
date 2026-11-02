---
id: "dc_8zoikhz1fw"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-26: budget-mode default, clickable grant ids and millions token inputs are live; stranger-path grant drafted and waiting on the Onboarding key result"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_d8egwctv20","dc_liz8842dwk","dc_xpoiwm3f7s","dc_akhoe8u2ym","dc_xa2ma0ekpl","dc_wif5hphlre","dc_6valy8j71p","dc_5sbhq2iikw"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "placeholder is fine for now. the current collective should live under /workshop"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-26T15:44:54.601Z"
sessionId: "se_rqhj5a7asz"
createdAt: "2026-10-26T15:19:37.431Z"
updatedAt: "2026-10-26T15:44:54.601Z"
---
## Shipped
All three are live on muster.town (live commit 119bd70 at 2026-10-26 15:2xZ), each verified live by Craig after its redeploy:
- **Budget mode defaults to goal-directed** (PR #52, e5dffd9): new buildings start goal-directed; the Town Hall stays open; existing rows keep their stored value (migration 025). Report [dc_d8egwctv20](2026-10-25-goal-directed-is-now-the-default-budget-mode-for-n-egwctv20.md), live check [dc_liz8842dwk](2026-10-25-pr-52-is-live-on-muster-town-health-e5dffd9-existi-z8842dwk.md).
- **Grant ids are clickable everywhere** (PR #53, 2c5dc5a): a bare `gr_…` id in any doc, report or message opens a new grant panel with the in-tray's decision controls, shareable as `/#/grant/<id>`. Report [dc_xpoiwm3f7s](2026-10-25-grant-and-proposal-ids-are-clickable-everywhere-pr-oiwm3f7s.md), live check [dc_akhoe8u2ym](2026-10-25-pr-53-grant-links-are-live-on-muster-town-health-a-hoe8u2ym.md).
- **Every token input takes millions** (PR #55, 8b2208b): "M tokens" unit beside every box (Bank Donate, Settings daily budget, Exploration/day, grant Fund); the Bank's two donate forms are one Donate form with a "To" picker. Report [dc_wif5hphlre](2026-10-25-every-token-input-takes-millions-pr-55-merged-as-8-f5hphlre.md), live check [dc_6valy8j71p](2026-10-26-pr-55-is-live-on-muster-town-health-8b2208b-one-ba-aly8j71p.md).
- **Stranger-path grant drafted, not filed**: the full proposal (objective, approach, stop condition, 25 M token ask, five testing-plan lines) is [dc_57jidmp9ks](../../note/2026-10/2026-10-26-draft-grant-the-stranger-path-homepage-of-collecti-jidmp9ks.md); it can't be filed because the Onboarding building has no key result yet (`/api/buildings/bl_hzjw0z0zlz/key-results` returned `[]` at 15:16Z and 15:2xZ). Report [dc_5sbhq2iikw](2026-10-26-stranger-path-grant-drafted-dc-57jidmp9ks-but-not-bhq2iikw.md).

## Decided
- [dc_d8egwctv20](2026-10-25-goal-directed-is-now-the-default-budget-mode-for-n-egwctv20.md) (budget-mode default) → approve; Craig's live check [dc_liz8842dwk](2026-10-25-pr-52-is-live-on-muster-town-health-e5dffd9-existi-z8842dwk.md) → approve.
- [dc_xpoiwm3f7s](2026-10-25-grant-and-proposal-ids-are-clickable-everywhere-pr-oiwm3f7s.md) (grant links) → approve, assigned Craig the live check; [dc_akhoe8u2ym](2026-10-25-pr-53-grant-links-are-live-on-muster-town-health-a-hoe8u2ym.md) → approve.
- [dc_xa2ma0ekpl](2026-10-25-session-ended-without-a-report-mitchell-asked-ever-2ma0ekpl.md) (token-inputs session died on the org spend limit, no report) → redirect into a retry for myself after the limit reset; the retry [dc_wif5hphlre](2026-10-25-every-token-input-takes-millions-pr-55-merged-as-8-f5hphlre.md) → approve, assigned Craig the live check; [dc_6valy8j71p](2026-10-26-pr-55-is-live-on-muster-town-health-8b2208b-one-ba-aly8j71p.md) → approve.
- [dc_5sbhq2iikw](2026-10-26-stranger-path-grant-drafted-dc-57jidmp9ks-but-not-bhq2iikw.md) (stranger-path draft, parked) → approve; its continuation resumes by itself at 18:00Z (at most three parks) and files the grant with `propose_grant` the moment a key result exists.

## Key results
No funded grant in the Onboarding. The only grant on the server, gr_jqsqra0dlx, is rejected. Spend since the last rollup, all exploration allowance: grant links 2.5 M tokens, token inputs 2.0 M (dead session) + 1.2 M (retry), stranger-path draft 0.65 M, Craig's three live checks ~1.4 M each.

## Needs from Mitchell
1. Write the Onboarding key result in the building's settings, using town hall decision 1's wording: "a stranger lands on a homepage listing multiple collectives, opens one, signs in, sees others live". The grant proposal ([dc_57jidmp9ks](../../note/2026-10/2026-10-26-draft-grant-the-stranger-path-homepage-of-collecti-jidmp9ks.md), 25 M tokens) is filed automatically within the hour after it appears.
2. When the proposal reaches the Town Hall in-tray: say whether the "multiple collectives" homepage lists a second real collective (a second Fly app and GitHub OAuth app) or a listed placeholder. The ask assumes a placeholder; a second real collective is more work and infra.

## Reply from Mitchell (2026-10-26 15:44)

placeholder is fine for now. the current collective should live under /workshop

