# RD Assistant

A Claude plugin for RD. Four skills that run against one person's own Microsoft
365 account and give that person their meetings, their correspondence and their
follow-ups back in a usable shape.

Owner: Karl Wakley. Version 1.0.0.

## Contents

```
rd-assistant/
  .claude-plugin/plugin.json
  config.md                          shared rules, read first by every skill
  setup-sheet.md                     the one page each user gets
  skills/
    week-ahead/                      scheduled, Monday 07:45
    todays-briefings/                scheduled, weekdays 08:00
    day-debrief/                     scheduled, weekdays 17:00
      references/recap-email.md
    post-call-followup/              on demand
```

## Install

1. Put this directory in the RD plugin marketplace repository.
2. Each user installs **RD Assistant** in Cowork and connects Microsoft 365
   themselves.
3. Hand each user `setup-sheet.md`.

## The permission model

The connector is set to draft and not send, and the plugin is written to stay
inside that rather than test it. `config.md` holds the allowed and not allowed
table, and every skill reads it first.

The only skills that write anything are `day-debrief`, `post-call-followup` and
`availability-sweep`, and all three write only Outlook drafts. Nothing creates a calendar event, posts to
Teams, or sends.

Teams is read only through the connector in any case. There is no post or reply
tool, which is why next-day reminders live in the debrief run output rather than
in a Teams message.

## Two design decisions worth knowing about

**Part D of the debrief.** A scheduled Cowork run cannot search Claude chat
history. Chat search is available on the web, desktop and mobile apps, and a
scheduled task is its own Cowork session. Memory is a partial substitute: it is
shared between chat and Cowork when Cowork runs in the cloud, and scheduled tasks
run remotely, so a scheduled run can see it. Memory holds durable facts rather
than a log of today, so it gives background and not "what I left unfinished".
The skill therefore uses memory where it is there, says so, and asks the user for
the rest.

On Team and Enterprise plans memory is off by default and an owner has to turn it
on in **Organization settings > Capabilities**. Until that happens the debrief
will report no memory context and go straight to the question, which still works.

**The naming rule.** The brief said no client names, no figures and no PII by
default. Taken literally that removes the point of a briefing about a meeting
with named people. `config.md` reads it as: these runs are private to one person
against their own mailbox, so attendees and their organisations are named, and
everything past that is out. No money in any form, no personal data beyond name,
role and organisation, no third parties who are not in the meeting, no
psychometrics on a named individual. If that reading is wrong, `config.md` is the
one file to change and every skill picks it up.

## The availability sweep

Added at JT's request, after the first four. Somebody emails asking for times, and
within the hour there is a reply draft in the thread with three or four slots that
are actually free.

It is not event driven. Nothing in Cowork fires on an email arriving, and an
Outlook rule cannot call Claude, so this is an hourly sweep. Worst case is a 59
minute delay and typical case is about half an hour, which still beats most
people.

Three mechanisms carry it:

- **No duplicates, no state file.** Before drafting, the skill checks the thread
  for an existing draft or a sent reply from the user, and skips if either is
  there. That is what stops ten runs a day producing ten copies, and it also
  stops the skill writing over a reply the user already sent themselves.
- **A 24 hour look back rather than a one hour window.** Missed runs and clock
  drift stop mattering, because re-reading the same email is free once the skip
  check is in place.
- **Ambiguous requests get listed, not drafted.** A booking link, a vague "we
  should catch up", somebody else on the thread being asked. The user reads four
  lines and says "that one as well". A draft nobody wanted costs more than a
  draft that was not written.

Tentative invites, focus time and blocked time count as busy and are never
offered. Slots start at least 24 hours out, four at most, across two or more
days, with 15 minutes clear either side of an existing meeting. Nothing is held,
so a slot can still be taken between the draft being written and the user sending
it. The draft says when the calendar was checked for that reason.

Where the sender proposed specific times, the reply answers those first and only
then offers alternatives. Ignoring somebody's suggested times and listing four
different ones is the most common way this kind of automation irritates people.

## Dependency to fix before the pilot

`rd-house-style/references/guardrails.md` item 7 still says Microsoft 365 is not
connected while the security review runs. It is connected. Any skill that reads
the house style will hedge against these four until that line changes. The same
text is inherited from `rd-outbound-pitch/references/guardrails.md`, so both need
editing.

## Pilot

Three users, one week. Worth watching:

- Whether people answer the three questions at the end of the debrief or ignore
  them. That is the difference between a report and an assistant, and it is the
  part most likely to fail.
- How many of the recap drafts actually get sent. A draft per meeting including
  internal ones is what was asked for. If people are deleting most of them by
  Wednesday, cut internal meetings out of Part B.
- Whether the three things to raise in the morning briefing hold up. The
  grounding rule says give two rather than invent a third, so count how often it
  gives two.
- Whether 17:00 is right. People who finish at 16:30 get an empty debrief.

The availability sweep is not part of the three user pilot. JT asked for it, so
run it on his account alone for the same week. Adding a fifth skill and a fourth
task to the pilot users mid-week costs more in muddied signal than it gains.
