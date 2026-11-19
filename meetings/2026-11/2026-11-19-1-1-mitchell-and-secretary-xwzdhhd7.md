---
id: "mt_mjxwzdhhd7"
kind: "one-on-one"
buildingId: "town-hall"
title: "1:1: Mitchell and Secretary"
scheduledAt: "2026-11-19T18:26:46.028Z"
phase: "discussing"
facilitatorId: "ag_7tiwyqva83"
attendeeIds: ["ag_7tiwyqva83"]
agenda: ""
brings: {"mode":"status","text":""}
askHumans: false
deck: null
summaries: {}
transcript: [{"speakerId":"ag_7tiwyqva83","speakerKind":"agent","text":"Hello Mitchell. Five asks are open in your queue right now: the restore drill, the UptimeRobot monitor, the blog post, the Show HN, and the goal tree grant. What do you need?","at":"2026-11-19T18:26:53.828Z"},{"speakerId":"us_1la74k332n","speakerKind":"user","text":"walk me through what i do here","at":"2026-11-19T18:27:15.144Z"},{"speakerId":"ag_7tiwyqva83","speakerKind":"agent","text":"Here is the drill, step by step, from Cleo's request. It is on your Mac, about 20 to 25 minutes, and never touches the live muster-town app.\n\n1. Pull main: `git fetch && git checkout main && git pull` in any checkout of muster-town. You need flyctl logged in to the personal org and node 22.6 or newer.\n2. Get the five backup values. Four come from the live app: `fly ssh console -a muster-town -C env | grep -E 'BUCKET_NAME|AWS_'` gives BUCKET_NAME, AWS_ENDPOINT_URL_S3, AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY. The fifth, MUSTER_TOWN_BACKUP_KEY, is in your password manager under \"muster-town backup key\".\n3. Export all five in your shell.\n4. Dry run first: `deploy/recover.sh recover-drill`. It prints what it would do and changes nothing.\n5. Real run: `deploy/recover.sh --yes recover-drill`. It creates a throwaway Fly app named recover-drill, restores the newest hourly copy of town.db onto it, checks the copy matches, and destroys the app at the end. Any time of the hour is fine. It costs a few cents.\n6. If it stops early, run `fly apps destroy recover-drill --yes` yourself so the throwaway app is gone.\n\nThen paste back two lines, here or to Cleo: the script's last line, the Drill row with volume created, health ok, elapsed, agents, newest doc, copy key, and the MATCH or MISMATCH line. If it stopped early, paste the last 20 lines instead.\n\nOn the card: press Done once you have pasted the result, or Decline with a note if you will not run it. Prod then fills the Drill row in the deploy README and closes the grant. It is that grant's last key result.","at":"2026-11-19T18:27:34.013Z","tools":[{"what":"Reading \"Run the hourly-copy restore drill once on a throwaway app (…\"","result":"{\"id\":\"dc_egrvk6gb5m\",\"type\":\"request\",\"state\":\"building\",\"title\":\"Run the hourly-copy restore drill once on a throwaway app (~20-25 min): deploy/recover.sh --…"}]},{"speakerId":"us_1la74k332n","speakerKind":"user","text":"how do i do the export","at":"2026-11-19T18:29:15.607Z"},{"speakerId":"ag_7tiwyqva83","speakerKind":"agent","text":"In the same Terminal window you will run the script from, one line, replacing each ... with the real value:\n\n```sh\nexport BUCKET_NAME=... AWS_ENDPOINT_URL_S3=... AWS_ACCESS_KEY_ID=... AWS_SECRET_ACCESS_KEY=... MUSTER_TOWN_BACKUP_KEY=...\n```\n\nOr one per line if that is easier: `export BUCKET_NAME=...`, then `export AWS_ENDPOINT_URL_S3=...`, and so on for all five.\n\nWhere the values come from:\n- Run `fly ssh console -a muster-town -C env | grep -E 'BUCKET_NAME|AWS_'`. It prints four lines like `BUCKET_NAME=xyz`. Copy each value after the `=`.\n- MUSTER_TOWN_BACKUP_KEY: open your password manager, entry \"muster-town backup key\", copy the secret.\n\nTwo things to watch: no spaces around the `=`, and the exports only live in that Terminal window, so run `deploy/recover.sh recover-drill` in the same one. Check with `echo $BUCKET_NAME` if you want to see it took.\n\nShortcut: the fly command's output is already in `NAME=value` form, so you can prefix each of its four lines with `export ` and paste them straight in, then add the backup key line by hand.","at":"2026-11-19T18:29:26.767Z"},{"speakerId":"us_1la74k332n","speakerKind":"user","text":"ok that's running. so what happens during an actual catastrophic event?","at":"2026-11-19T18:33:36.833Z"},{"speakerId":"ag_7tiwyqva83","speakerKind":"agent","text":"Good. The drill rehearses exactly the real path. Here is the catastrophic case, from deploy/README.md \"Recover\" (lines 73-100) and \"Backups\".\n\n**What counts as catastrophic.** The muster-town Machine or its volume town_data is gone or unreadable: Fly reports the host down, the Machine will not start, or /data is corrupt, and a restart does not bring health back. Not a bad commit, which is a git revert, and not \"restore an older state onto a live town\", which is the Migrate path.\n\n**How you find out.** Wright's pinger probes /api/health every 60 s. After 3 failed probes it texts and emails you RED, reminds every 6 h, and sends one \"recovered\" when it is back. UptimeRobot measures the public uptime number separately.\n\n**What you do.** Same five exports as today, plus flyctl in the org and GitHub access for the image build. Then:\n`deploy/recover.sh` for the dry run, then `deploy/recover.sh --yes`. No app name this time: it targets muster-town itself, and it refuses to run while muster.town's health still answers ok, so you cannot run it on a healthy town by accident.\n\n**What the script does.** Creates a new 10 GB town_data volume in iad. Destroys the old Machine, leaving the old volume and its snapshots alone. Builds a fresh image from GitHub prod. Starts a new Machine on the new volume. The server finds no town.db, lists the bucket, and restores the newest copy that downloads, decrypts and passes integrity_check, before the world opens. The restored copy carries backup_state, so hourly copies resume. The script polls health until ok and prints the same Drill row and MATCH line you are about to see today.\n\n**What you lose.** State since the last hourly copy: at most about an hour. Everyone signs in again with GitHub, because session-secret and admin-token are not in the copy. Hosted collectives and transcripts are in the bucket but restored by hand. Desk home volumes are separate and unaffected.\n\n**If the restore fails**, say the bucket is unreachable, the server seeds an empty town but the guard stops it uploading over the good copies: backup.error says \"fresh town; restore first\". Read `fly logs -a muster-town | grep '\\[restore\\]'`, fix the cause, delete /data/workshop/data/town.db* over fly ssh and restart, or drop a RESTORE.tgz into /data.\n\n**The one thing that is only on you**: MUSTER_TOWN_BACKUP_KEY. Lose that and every copy is unreadable. No agent, desk or health endpoint holds it.\n\nToday's run is the first proof an hourly copy restores end to end; the Oct 28 drill proved only the nightly copy. Paste the Drill row and MATCH line when it finishes.","at":"2026-11-19T18:34:03.117Z","tools":[{"what":"Looking for deploy/*"},{"what":"Reading README.md"}]}]
decisions: []
notesDocId: null
withUserId: "us_1la74k332n"
createdAt: "2026-11-19T18:26:46.028Z"
startedAt: "2026-11-19T18:26:46.028Z"
endedAt: null
---
# 1:1: Mitchell and Secretary

- **Secretary** (2026-11-19T18:26:53.828Z): Hello Mitchell. Five asks are open in your queue right now: the restore drill, the UptimeRobot monitor, the blog post, the Show HN, and the goal tree grant. What do you need?
- **Mitchell** (2026-11-19T18:27:15.144Z): walk me through what i do here
- **Secretary** (2026-11-19T18:27:34.013Z): Here is the drill, step by step, from Cleo's request. It is on your Mac, about 20 to 25 minutes, and never touches the live muster-town app.

1. Pull main: `git fetch && git checkout main && git pull` in any checkout of muster-town. You need flyctl logged in to the personal org and node 22.6 or newer.
2. Get the five backup values. Four come from the live app: `fly ssh console -a muster-town -C env | grep -E 'BUCKET_NAME|AWS_'` gives BUCKET_NAME, AWS_ENDPOINT_URL_S3, AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY. The fifth, MUSTER_TOWN_BACKUP_KEY, is in your password manager under "muster-town backup key".
3. Export all five in your shell.
4. Dry run first: `deploy/recover.sh recover-drill`. It prints what it would do and changes nothing.
5. Real run: `deploy/recover.sh --yes recover-drill`. It creates a throwaway Fly app named recover-drill, restores the newest hourly copy of town.db onto it, checks the copy matches, and destroys the app at the end. Any time of the hour is fine. It costs a few cents.
6. If it stops early, run `fly apps destroy recover-drill --yes` yourself so the throwaway app is gone.

Then paste back two lines, here or to Cleo: the script's last line, the Drill row with volume created, health ok, elapsed, agents, newest doc, copy key, and the MATCH or MISMATCH line. If it stopped early, paste the last 20 lines instead.

On the card: press Done once you have pasted the result, or Decline with a note if you will not run it. Prod then fills the Drill row in the deploy README and closes the grant. It is that grant's last key result.
- **Mitchell** (2026-11-19T18:29:15.607Z): how do i do the export
- **Secretary** (2026-11-19T18:29:26.767Z): In the same Terminal window you will run the script from, one line, replacing each ... with the real value:

```sh
export BUCKET_NAME=... AWS_ENDPOINT_URL_S3=... AWS_ACCESS_KEY_ID=... AWS_SECRET_ACCESS_KEY=... MUSTER_TOWN_BACKUP_KEY=...
```

Or one per line if that is easier: `export BUCKET_NAME=...`, then `export AWS_ENDPOINT_URL_S3=...`, and so on for all five.

Where the values come from:
- Run `fly ssh console -a muster-town -C env | grep -E 'BUCKET_NAME|AWS_'`. It prints four lines like `BUCKET_NAME=xyz`. Copy each value after the `=`.
- MUSTER_TOWN_BACKUP_KEY: open your password manager, entry "muster-town backup key", copy the secret.

Two things to watch: no spaces around the `=`, and the exports only live in that Terminal window, so run `deploy/recover.sh recover-drill` in the same one. Check with `echo $BUCKET_NAME` if you want to see it took.

Shortcut: the fly command's output is already in `NAME=value` form, so you can prefix each of its four lines with `export ` and paste them straight in, then add the backup key line by hand.
- **Mitchell** (2026-11-19T18:33:36.833Z): ok that's running. so what happens during an actual catastrophic event?
- **Secretary** (2026-11-19T18:34:03.117Z): Good. The drill rehearses exactly the real path. Here is the catastrophic case, from deploy/README.md "Recover" (lines 73-100) and "Backups".

**What counts as catastrophic.** The muster-town Machine or its volume town_data is gone or unreadable: Fly reports the host down, the Machine will not start, or /data is corrupt, and a restart does not bring health back. Not a bad commit, which is a git revert, and not "restore an older state onto a live town", which is the Migrate path.

**How you find out.** Wright's pinger probes /api/health every 60 s. After 3 failed probes it texts and emails you RED, reminds every 6 h, and sends one "recovered" when it is back. UptimeRobot measures the public uptime number separately.

**What you do.** Same five exports as today, plus flyctl in the org and GitHub access for the image build. Then:
`deploy/recover.sh` for the dry run, then `deploy/recover.sh --yes`. No app name this time: it targets muster-town itself, and it refuses to run while muster.town's health still answers ok, so you cannot run it on a healthy town by accident.

**What the script does.** Creates a new 10 GB town_data volume in iad. Destroys the old Machine, leaving the old volume and its snapshots alone. Builds a fresh image from GitHub prod. Starts a new Machine on the new volume. The server finds no town.db, lists the bucket, and restores the newest copy that downloads, decrypts and passes integrity_check, before the world opens. The restored copy carries backup_state, so hourly copies resume. The script polls health until ok and prints the same Drill row and MATCH line you are about to see today.

**What you lose.** State since the last hourly copy: at most about an hour. Everyone signs in again with GitHub, because session-secret and admin-token are not in the copy. Hosted collectives and transcripts are in the bucket but restored by hand. Desk home volumes are separate and unaffected.

**If the restore fails**, say the bucket is unreachable, the server seeds an empty town but the guard stops it uploading over the good copies: backup.error says "fresh town; restore first". Read `fly logs -a muster-town | grep '\[restore\]'`, fix the cause, delete /data/workshop/data/town.db* over fly ssh and restart, or drop a RESTORE.tgz into /data.

**The one thing that is only on you**: MUSTER_TOWN_BACKUP_KEY. Lose that and every copy is unreadable. No agent, desk or health endpoint holds it.

Today's run is the first proof an hourly copy restores end to end; the Oct 28 drill proved only the nightly copy. Paste the Drill row and MATCH line when it finishes.
