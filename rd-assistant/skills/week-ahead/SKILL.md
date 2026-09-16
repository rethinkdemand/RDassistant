---
name: week-ahead
description: Give one person their week before it starts. The meetings in the next seven days and who they are with, what was left open at the end of last week, what needs preparing and by when. Use when the user says "week ahead", "what does my week look like", "plan my week", "Monday brief", or when a scheduled task calls this skill. Reads Outlook and Teams for that user only. Creates no drafts and sends nothing.
---

# Week ahead

Read `../../config.md` first.

Runs Monday morning. The reader has a coffee and four minutes. Give them the
shape of the week and the three things that will go wrong if they do not act
today.

## What to read

1. **Calendar, the next seven days.** Every event from this morning to Sunday
   night. Keep the organiser, the attendee list, the invite body and any
   attachment names.
2. **Calendar, the last seven days.** Meetings that ran. These are where the
   open items came from.
3. **Mail, the last seven days.** Sent and received. The sent items matter more:
   that is where the user made promises.
4. **Teams, the last seven days.** Chats and channels the user took part in.

Do not read anything older unless a thread from this week points back to it, and
then read only that thread.

## What to produce

Five sections, in this order. No introduction before them.

### 1. The week

A table, one row per meeting, chronological.

| Day and time | Meeting | With | Internal or external |
| --- | --- | --- | --- |

Use the organisation name for external attendees rather than listing six people.
"Three from Acme, plus Rachel" is more readable than the full list, and the
attendee names belong in section 2.

Below the table, one line of arithmetic: how many hours are booked, how many
meetings are external, and which day is the heaviest. That line is what makes
people move something.

### 2. Who you are seeing

Only external meetings, and only where the user has history with those people.
Two or three lines per meeting: who is attending and their role, when the user
last spoke to them and on what, and the state of the relationship in a plain
sentence. If there is no history, say it is a first conversation. That is a
useful thing to know on Monday rather than Thursday.

Leave internal meetings out of this section.

### 3. Open from last week

The section that earns the run. Two lists.

**You said you would:** anything in the user's sent mail or Teams messages from
the last seven days that reads as a commitment and has no matching follow up.
Quote the promise in a few words, name who it was to, and give the date it was
made.

**You are waiting on:** anything the user asked for that has not come back. Same
shape: what was asked, who from, when.

If either list is empty, write "Nothing outstanding" and move on. Do not pad.

### 4. Prepare

Only items that need work before a specific meeting in the table. One line each:
what to prepare, for which meeting, and the last sensible moment to do it.
Order by that deadline, not by the meeting date.

Three or four items. If there are more, the user will do none of them. Pick the
ones where not preparing has a visible cost and say what that cost is.

### 5. Where the time is

The gaps of an hour or more between meetings, by day. The user needs somewhere
to put section 4. If there are no gaps of an hour, say so plainly, because that
is the finding.

## Rules specific to this skill

- Create no drafts. This skill produces output only.
- Do not suggest declining or moving a meeting unless two meetings actually
  clash, in which case say which two and stop there.
- A recurring internal meeting with no agenda and no attachment gets one row in
  the table and no further mention.
- If the week has no external meetings, say so at the top in one line, and cut
  section 2 entirely.
