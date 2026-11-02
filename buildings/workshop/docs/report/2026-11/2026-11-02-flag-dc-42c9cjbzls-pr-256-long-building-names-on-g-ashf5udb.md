---
id: "dc_48ashf5udb"
type: "report"
state: "building"
title: "Flag dc_42c9cjbzls: PR #256 (long building names on goal boxes + Haiku-named new buildings) open, parked on CI"
authorId: "ag_b18cwyner4"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #256 built both asks of flag dc_42c9cjbzls; the continuation as_nme0wvlz9p is already queued on {pr: 256} (merge if green, redeploy, guest live-check, Haiku-name check, rollup 38 line). Nothing more to queue; it goes in rollup 38 once live."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-02T02:34:02.934Z"
sessionId: "se_w19j5xst1k"
assignmentId: "as_vb0pp1reo5"
costUsd: 2.1036143000000003
tokens: 105181
turns: 53
createdAt: "2026-11-02T02:33:53.876Z"
updatedAt: "2026-11-02T02:34:02.934Z"
---
## What I did
Built both asks from Mitchell's flag [dc_42c9cjbzls](../../flag/2026-11/2026-11-01-the-desk-add-and-remove-on-goal-nodes-in-the-goal-c9cjbzls.md) as one PR, https://github.com/mitchellgordon95/muster-town/pull/256 (branch head is a merge of main, made after a `docs/log.md` conflict; GitHub reports it MERGEABLE and CI is running). Parked on `{pr: 256}`.

## Findings
- **Long names (ask 1)**: in `GoalCanvas.tsx` each building row is now `− <span.gc-bname>name</span> <span.gc-bn>· n</span> +`. The CSS (`styles.css`) clips the name with an ellipsis, and the tag's title tooltip still holds the full name. The count and the −/+ buttons can't shrink: − sits on the left and + at the row's right edge, so the controls line up across rows. Guests see the same ellipsis without buttons. I checked it with a headless Chromium render of the real stylesheet using "People who would use Muster Town know…" (desk ~/shots/gc/t.png). Not checked yet: live, and Fit at low zoom (the canvas just scales a fixed layout, so it should hold).
- **Haiku naming (ask 2)**: when `POST /api/buildings` gets no name, it now calls the new runtime hook `RuntimeHooks.nameBuilding` (`packages/runtime/src/naming.ts`). That makes one `oneShot` call on the building's `cheapModel` (Haiku). The call is funded with `fundingFor(manager, cheapModel)` and booked on the new manager as a session with the new purpose `naming` (`chargeUsage`, plus a funders label "building naming"). A cleaned answer of 1–4 words and at most 32 characters renames the building. In every other case the goal's short text stays: the call fails, the answer is unusable, the Bank has no credential (`NoCredential`), or the hook throws. The response carries the chosen name, so the canvas toast and the reloaded tree show it right away.
- **Design choice for you to know about**: I deliberately skipped the `budget.canStart` gate. A building made a moment ago in this goal-directed town has no daily room, so with the gate the call would never run live. The call costs a few hundred tokens and is booked like any host call.
- **Tests**: runtime `test/naming.test.ts` has 5 tests (rename + booked session on the manager + model, failed call, unusable answer, no credential → no call, `cleanBuildingName`). Server `rest.test.ts` has a new test (a blank name uses the hook, a typed name skips it, a throwing hook keeps the goal text). `npm run check --fast` passed: docs, typecheck, and the affected tests (web 160/160; runtime and server green). Docs updated: goals.md, architecture.md, log.md. There is no migration (session `purpose` is a free TEXT column).
- **Plan for the continuation**:
  1. If CI is green, merge #256 and redeploy.
  2. As a guest on the live editor, check the long-name row and Fit at low zoom.
  3. As admin, press + on a throwaway goal to check the Haiku name and the `naming` session. The agent token may lack `town.manage_buildings`; if so, say it.
  4. Add a Shipped candidate to [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md), then update topic page [dc_hsq0e5a587](../../wiki/2026-10/2026-10-31-goal-tree-editor-ux-flag-dc-yn8gl1rmyt-q0e5a587.md).

## What I need from you
Nothing needed.
