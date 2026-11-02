---
id: "dc_wdwenovz65"
type: "report"
state: "building"
title: "Plain words in report, meeting and building panels: PR #268 open, parked on CI"
authorId: "ag_vjdbpap751"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Good scope. Merge/redeploy continuation as_g8qxiuhp4p is already queued; it stays held until Mitchell decides the checkpoint (dc_mmf9y841v1)."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-02T18:10:57.272Z"
sessionId: "se_aaj1epsoud"
assignmentId: "as_x938cqhjrg"
costUsd: 1.2634927999999999
tokens: 63175
turns: 42
createdAt: "2026-11-02T18:08:19.694Z"
updatedAt: "2026-11-02T18:10:57.272Z"
---
## What I did
- Ran the delight-walk (script from PR #211's branch, skill [dc_14la62qft8](../../skill/2026-10/2026-10-31-delight-walk-la62qft8.md)) on live 5265d70 at 1280×720 and 390×844 to get the "before" numbers.
- Opened PR #268 (https://github.com/mitchellgordon95/muster-town/pull/268) and marked it ready. Typecheck, `npm run check --fast` and web tests (253/253) all pass locally. I didn't touch the agent panel.

## Findings
The PR changes:
- **Meeting title:** `nameOf` now turns a `us_` id into the name of that human's avatar in the snapshot, which carries `ownerUserId`. Live has Mitchell as us_1la74k332n, so "1:1 · Town Workshop · us_1la74k332n and ★ Pix" will read "… Mitchell and ★ Pix". This also fixes `us_` ids anywhere else `nameOf` is used.
- **Report panel:**
  - "$0.50 · 25k adj. tokens · 8 turns" becomes "$0.50 of work · 8 steps". Adjusted tokens and turns move to the tooltip.
  - "[dc_es3linx30i](2026-11-02-pr-211-delight-walk-script-marked-ready-main-merge-3linx30i.md) ⧉" becomes a "Copy link" button, with the id in its tooltip.
  - Bare `dc_` ids in a body now show the doc's title. If the doc isn't loaded, it's fetched once, using the same path that already labels `as_`/`mt_` ids. The id is in the tooltip. This changes the old "dc_ links show the id" design choice, as the assignment asked.
- **Building panel:**
  - "Adj. tokens used" becomes "Work done: X tokens today · Y in all".
  - "In-tray: worked by ★ Kelly" becomes "Reports: ★ Kelly reads and decides them".
  - "Walk to the in-tray" becomes "Walk to the manager's desk (reports to read)".

Jargon lines before the change (live 5265d70, one run; laptop / phone):

| moment | laptop | phone | what was flagged |
|---|---|---|---|
| report | 5/56 | 5/47 | cost line, "dc_… ⧉", plus body text ("parked", "as_…") |
| meeting | 6/52 | 5/41 | us_ title, plus transcript text ("in-tray", "gr_xxx") |
| building | 4/61 | 3/50 | "Walk to the in-tray", "Adj. tokens used", "In-tray worked by", map bubble |

What I expect after: about 2–3 fewer lines per moment. The rest is agents' own wording in report bodies and transcripts ("parked", "in-tray"), which a UI change can't fix. The after-run happens once the change is live.

## What I need from you
Nothing needed. I resume when PR #268's CI finishes, then merge, redeploy and re-run the walk.
