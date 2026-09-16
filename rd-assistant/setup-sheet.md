# RD Assistant: set yours up in ten minutes

It reads your Outlook and Teams, and nobody else's. It writes drafts. It cannot
send anything.

## Before you start (about 4 minutes)

1. Open Claude Desktop. If you cannot see **Cowork** in the left sidebar, message
   Karl. An admin has to switch it on for you.
2. Connect Microsoft 365: **Settings > Connectors > Microsoft 365 > Connect**.
   Sign in with your RD account and accept the permissions.
3. Install the **RD Assistant** plugin from the RD marketplace.

## Create three scheduled tasks (about 6 minutes)

For each row below: click **Scheduled** in the left sidebar, then **New task**,
paste the prompt, set the cadence and time, save.

| Task name | When | Paste this |
| --- | --- | --- |
| Week ahead | Weekly, Monday, 07:45 | Run the rd-assistant week-ahead skill for my week. Read my Outlook calendar, mail and Teams for the last seven days and the next seven days. Output only, no drafts. |
| Today's briefings | Weekdays, 08:00 | Run the rd-assistant todays-briefings skill for today. One briefing per external meeting. If I have no external meetings today, say so in one line and stop. |
| Day debrief | Weekdays, 17:00 | Run the rd-assistant day-debrief skill for today. Create the recap drafts in Outlook and finish with the three questions. Do not send anything. |

That is the setup finished.

**Optional fourth task, if people ask you for times a lot.** Same steps, one more
row.

| Task name | When | Paste this |
| --- | --- | --- |
| Availability sweep | Hourly, weekdays, 08:00 to 18:00 | Run the rd-assistant availability-sweep skill. Check my mail from the last 24 hours for anyone asking me for times, draft replies in the thread with my actual free slots, and skip anything I have already replied to. Do not send and do not put anything in my calendar. |

It runs ten times a day and most runs will find nothing and say so. When somebody
does ask for a call, a reply draft with three or four real free times is waiting
within the hour. It will not offer anything you have marked tentative, blocked or
out of office, and it never holds a slot, so check the times still work before
you send.

## What you get back

**Monday 07:45, Week ahead.** Your meetings for the week in a table, who the
external ones are with and when you last spoke to them, what you promised
somebody last week and have not done, what needs preparing and by when, and
where the free hours are.

**Weekdays 08:00, Today's briefings.** One short briefing per external meeting:
who is in the room, the last email and Teams exchange with them, what is still
open, and three things to raise. No external meetings today means one line and
nothing else.

**Weekdays 17:00, Day debrief.** What happened today, a recap email **draft** in
your Outlook drafts for every meeting that ran, what is waiting on a reply in
both directions, then three questions. Answer them in the task whenever you get
to it, from your phone if you like. Anything you want flagged for tomorrow gets
written into that run, so you find it there in the morning.

The drafts are drafts. Read them, change what you want, press send yourself.

## The fourth one, when you want it

After a call, open a normal Cowork task and paste your notes or the transcript
with: **follow up on this call**. You get a recap email draft in Outlook and an
action list with owners and dates. No setup needed.

## If something looks wrong

- **Nothing ran.** Check **Scheduled** in the sidebar for the last run. Tasks run
  remotely, so your laptop being shut is not the cause.
- **It says it cannot reach your mail.** Reconnect Microsoft 365 in Settings.
- **It got something wrong.** Reply in the run and tell it. It will correct the
  draft.
- **It made something up.** Screenshot it and send it to Karl. That is the one
  thing worth interrupting him for.

## What it will not do

It will not send an email, post in Teams, put anything in your calendar, or
touch anyone else's mailbox. It leaves client figures out of everything on
purpose, so where a number mattered it points you at the thread instead.
