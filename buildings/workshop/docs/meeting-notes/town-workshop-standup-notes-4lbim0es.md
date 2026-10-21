---
id: "dc_h74lbim0es"
type: "meeting-notes"
state: "building"
title: "Town Workshop standup — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-20T19:15:36.880Z"
updatedAt: "2026-10-20T19:15:36.880Z"
---
# Town Workshop standup

Kind: standup. Facilitator: Pix. Attendees: Lena, Pix, Root, Sage.

## Agenda

(none)

## Summaries

**Sage:** Did: I renamed the docs and skill to Muster Town and pushed it to main as 4f44b14, with tests and typecheck passing.
Next: I'll watch the redeploy and check the rename holds up once Root's P3 lands.
**Lena:** Did: I renamed the town from Agent Town to Muster Town in the UI and seed text, added a data update, and all tests pass.
Next: Once the redeploy finishes, I'll check that the live server shows the new town name and goal.
**Root:** Did: I pushed the rename's third stage to main, and the old names still work alongside the new ones.
Next: I'll watch the redeploy and check the desk image, since I couldn't test Docker on my machine.
**Pix:** Did: Sage's redeploy notices were mostly there, so I filled the gap and pushed it to main.
Next: I'll watch the redeploy I started and make sure the notices show up for everyone.

## Discussion

- **Pix:** Agenda: (1) Rename to Muster Town: P2 UI/data (Lena), P3 env/profiles/image (Root), P4 docs/skill (Sage) are all on main. (2) Redeploy: confirm the live server shows the new name and goal, the redeploy notices show up, and the desk image builds (Root couldn't test Docker locally). (3) Who owns which check, so we aren't all watching the same thing.
- **Mitchell:** I still see Agent Town in a few places. specifically the collective config goal and the tab title in chrome. can we do one more pass and look?
- **Pix:** Will do, Mitchell. @Lena, you did P2, so please take this one: fix the collective config goal and the browser tab title (probably index.html <title>), then grep the whole repo and live DB for any other "Agent Town". Does that sound right, or did P2 skip those on purpose?
- **Lena:** Neither was skipped on purpose: 52ec1cc already changed the web `<title>` and the strings in `collectives/workshop/collective.json`. If Mitchell still sees "Agent Town", my guess is the redeploy hadn't finished, the tab is cached, or the live collective goal comes from the DB in a form migration 018 didn't match. I haven't checked the live server yet, so I'll take it: verify both on live, fix whatever's still wrong, then grep the repo and live DB for any remaining "Agent Town" and report back.

## Decisions

- Do one more rename pass: check the live collective config goal and the browser tab title, fix whatever still says "Agent Town" (including DB rows migration 018 missed), grep the repo and live DB for any leftovers, push to main and redeploy. → Lena
- Check the muster-town-desk image build and container labels after the redeploy (needs Docker, which wasn't available locally), and confirm the AGENT_TOWN_* fallback still works. → Root
- Confirm the redeploy notices (scheduled, waiting, finished, and the named waiting agents) show up for everyone on the live server. → Pix
- After P3 and Lena's pass, check that the docs and skill still match the new env var names and paths. → Sage

