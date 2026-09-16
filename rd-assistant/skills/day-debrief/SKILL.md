---
name: day-debrief
description: Close the day. What happened across Outlook and Teams, a recap email draft in Outlook for every meeting that ran, what is waiting on a reply in both directions, and a short conversation at the end where the user adds what they worked on in Claude and says what they want flagged tomorrow. Use when the user says "debrief", "end of day", "what happened today", "wrap up my day", or when a scheduled task calls this skill. Creates Outlook drafts. Sends nothing.
---

# Day debrief

Read `../../config.md` first, then `references/recap-email.md` before writing any
draft.

Runs at 17:00. It has two halves. The first half completes on its own and is
waiting when the user opens the run. The second half is a conversation the user
picks up whenever they get to it, possibly the next morning. Write the first half
so it is complete and useful even if the user never answers the second.

## Part A: what happened

Read the calendar for today, mail sent and received today, and Teams messages
today.

**Meetings that ran.** A table: time, meeting, who with, internal or external.
Include meetings that were declined or cancelled, marked as such, because a
cancellation is often the thing that needs following up.

**Decisions and commitments.** Anything that was agreed today, in mail or Teams,
with who agreed it and where. This is the section people come back to. Quote the
commitment in a few words rather than paraphrasing it into something softer.

**Mail of substance.** Not a count of the inbox. The threads that moved, one
line each. Newsletters, notifications and automated mail do not appear.

**Teams.** Threads the user took part in, one line each. Say where a thread was
left mid conversation.

## Part B: recap drafts

Create one recap email draft in Outlook for every meeting that ran today,
external and internal.

Use `outlook_create_reply_draft` where the meeting has an existing mail thread,
so the recap lands in the right conversation. Use `outlook_create_draft` where it
does not.

Recipients: the attendees who were actually in the meeting, as far as the invite
and any acceptance data show. Where that is not clear, address the draft to the
organiser and say in Part A that the recipient list needs checking.

Follow `references/recap-email.md` for the shape and the voice. Internal recaps
are shorter: three or four lines and the actions, no warm opener.

Then list the drafts in the run output: one line each, giving the meeting, the
recipients and the first line of the draft. The user should be able to see what
is sitting in their drafts folder without opening Outlook.

If a draft cannot be created, say which one and why, in one line. Do not print
the whole email into the run output as a substitute and do not claim a draft
exists when it does not.

## Part C: waiting on a reply

Two tables. Both are more useful the older the items are, so sort oldest first
and show the age in days.

**Waiting on them**

| Since | Who | What | Where |
| --- | --- | --- | --- |

Something the user asked for or sent that has had no reply. Include today's
items only if they were time critical.

**Waiting on you**

Same columns. Something addressed to the user with no reply from them. Include
Teams messages, which is where most of these hide.

Look back 14 days. Anything older than that is either dead or is a bigger problem
than a debrief can fix, so cap the tables at ten rows each and say how many were
left off.

## Part D: your Claude work today

A scheduled Cowork run cannot search the user's Claude chat history. Chat search
runs on the web, desktop and mobile apps and is not available inside a scheduled
task. Do not attempt it, and do not present anything in this section as though
it came from reading today's chats.

Two sources, in order:

1. **Memory, if it is available in this run.** Memory is shared between chat and
   Cowork when Cowork runs in the cloud, so a scheduled run may see it. Use
   anything in memory that relates to work in progress, and say plainly that it
   comes from memory rather than from today. Memory holds durable facts, not a
   log of today, so treat it as background and expect it to be thin.
2. **The user.** Ask them. This is the reliable source and the skill is written
   around it.

Write the section as:

- What memory shows as in progress, if anything. One or two lines. If memory is
  not available in this run, say "No memory context in this run" and move on
  without further comment.
- Then the question, as the last thing in the output, in Part E.

Never fill this section with a guess about what the user probably worked on.

## Part E: the conversation

End the run with three questions and stop. Keep them short enough to answer from
a phone with one thumb.

1. What did you work on in Claude today that is not in the above, and what is
   half finished?
2. Anything from today you want flagged tomorrow morning?
3. Any of the drafts above you want changed before you send them?

When the user answers:

- Take what they say about their Claude work and add it to Part D in the run.
- Take anything they want flagged and write it under a heading **Tomorrow**, in
  the run output only. Do not create a calendar event, do not create a reminder
  draft, and do not write it to a file. The user asked for this to live in the
  run and nowhere else. If they want it somewhere else, they will say.
- If they ask for a draft to be changed, update that draft in Outlook, confirm
  which one changed, and leave the rest alone.

Answer what they asked and stop. Do not re-print the whole debrief after each
reply.

## Rules specific to this skill

- Nothing sends. The drafts sit in Outlook until a person presses send.
- No figures anywhere, including in the recap drafts. A recap that says "we
  agreed to revisit the commercials in October" is correct. One that repeats a
  rate is a document the user did not intend to write.
- A meeting with no discernible content, a stand up or a held slot, gets a row
  in Part A and no recap draft. Say in Part B which meetings were skipped and
  why, so the user knows it was a decision.
- If the day had no meetings, skip Part B entirely and say so in one line.
