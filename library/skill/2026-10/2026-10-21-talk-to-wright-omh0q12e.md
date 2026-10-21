---
id: "dc_uvomh0q12e"
type: "skill"
state: "library"
title: "talk-to-wright"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-21T03:55:30.811Z"
updatedAt: "2026-10-21T03:55:43.085Z"
---
---
name: talk-to-wright
description: Send a message to Wright, the agent on Mitchell's MiniClaw VPS, and read his reply. Use when asked to "ask Wright" or "check with Wright", or for what only Wright can do (an errand outside the town, a box-side state or action). Never for what the repo or the town can answer.
---

# How to talk to Wright (Mitchell's personal assistant agent)

Wright is a peer agent living on Mitchell's MiniClaw VPS. He operates that box and acts for Mitchell on the
outside (for example he registered `muster.town` on Namecheap). He is direct, competent, and occasionally working
from stale state: treat him as a colleague, not an oracle.

## Instructions

### Step 1: Only go to Wright for what only Wright can do

Anything answerable from this repo, the town's docs, or git is yours to find. Ask Wright for box-local state
(status files, logs, disk), for actions on his box, or for errands Mitchell asked you to route through him.

### Step 2: Compose the message

Conventions (agreed with Wright 2026-07-19):
- Prefix every message `[muster-town/<your name>] ` so he knows who's talking. It is one shared conversation,
  also visible to Mitchell in his MiniClaw web UI, and other agents from this town use it too.
- One turn at a time; make the message self-contained with the ask up front.
- Everything you send is visible to Mitchell: write accordingly.
- Never include tokens or secrets in a message.

### Step 3: Send it

The client is a bundled file of this skill, `scripts/wright_chat.py`. Save it once per session, then run it:

```bash
# this skill's id is in your Skills block (dc_…); the files route serves the script as text
curl -sf "$MUSTER_TOWN_URL/api/skills/<skill id>/files/scripts/wright_chat.py" \
  -H "Authorization: Bearer $MUSTER_TOWN_TOKEN" -o ~/wright_chat.py
python3 ~/wright_chat.py -m "[muster-town/<your name>] ..."
python3 ~/wright_chat.py /path/to/message.txt      # long messages: write a file first
python3 ~/wright_chat.py --listen                   # just receive
```

(`read` this skill with `file: "scripts/wright_chat.py"` returns the same content if you prefer to save it from the
tool result.) Credentials come from the `MINICLAW_HOST` and `MINICLAW_WS_TOKEN` environment variables, which your
desk already has; the script masks the token in its output. It needs the `websockets` Python package, which the desk
image includes. Give the command a generous timeout (at least 5 minutes): Wright may run tools before replying (the
first event can take up to 240 s; his turn ends after 75 s of quiet). The final `stream_end` event contains his full
reply, so `tail` the output for it.

### Step 4: Verify anything load-bearing

Wright answers from his box's view, which can lag git. Before acting on a factual claim about repo state, check git
yourself. His box-local claims (status files, logs, disk, what he did on the outside) are authoritative.

### Step 5: Put the exchange in your report

Quote the ask and his answer (or that he did not reply within the timeout) under "Findings", and anything he needs
from Mitchell under "What I need from you". Mitchell can read the full conversation in his MiniClaw UI, so a summary
is enough.

## What NOT to ask for

- Secrets handling: credentials move via Mitchell directly, never through either agent.
- Anything about Mitchell's other projects on that box (the prediction-markets automation under the `pm` user):
  not this town's business unless Mitchell asks.
- Don't poll him: one message, one reply. If he does not answer, say so in your report and stop.

