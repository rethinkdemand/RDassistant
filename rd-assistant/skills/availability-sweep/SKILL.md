---
name: availability-sweep
description: Find emails asking the user for times, check the calendar, and leave a reply draft in Outlook offering real free slots. Use when the user says "anyone asking for time", "check for meeting requests", "draft my availability replies", or when a scheduled task calls this skill. Runs hourly on weekdays. Reads mail and calendar, writes reply drafts only. Never sends, never holds a slot, never creates a calendar event.
---

# Availability sweep

Read `../../config.md` first.

Somebody asks for a call. Within the hour there is a reply draft in Outlook with
three or four times that are actually free. The user reads it, presses send.

This skill is not live. It runs on a clock and catches what arrived since the
last run. Do not describe it to anyone as instant.

## Window

Read mail received in the last 24 hours, not the last hour. Runs get missed and
clocks drift, and the duplicate check below makes overlap harmless. It is better
to look at the same email twice and skip it than to miss it once.

Both internal and external senders.

## What counts as a request

Draft only where the sender is clearly asking the user for times. These qualify:

- A direct ask. "When are you free next week", "what does your diary look like",
  "let me know some times".
- A specific proposal. "Does Tuesday at 10 work for you". This is a different
  reply and is handled below.
- A request to move an existing meeting to a new time.

These do not, and get listed in the run output with one line saying why, no
draft:

- A booking link in the message or signature. The sender wants them to use it.
- A meeting invite. That is an accept or decline, which is a calendar action and
  out of scope.
- Somebody else on the thread being asked, not the user.
- "We should catch up sometime" with no request attached.
- Anything you are not confident about.

The run output list is the point of this rule. The user reads four lines, says
"that one as well", and you draft it. That is cheaper for them than deleting
drafts they did not want.

## Skip anything already handled

Before drafting, check the conversation for either of these:

1. A draft in that thread, from any source including this skill on an earlier
   run.
2. A sent reply from the user after the request arrived.

If either exists, skip it and say nothing in the output. This is what stops the
hourly cadence producing eight copies of the same draft, and it also stops the
skill writing over a reply the user has already handled themselves.

## Choosing slots

Use `outlook_find_available_time` for the user alone, or
`find_meeting_availability` where the request names other RD people who need to
be in the room.

Rules for what counts as free:

- **Tentative invites, focus time, blocked time and out of office are busy.**
  Never offer a slot that sits on one. The user blocked it for a reason and a
  reply that offers it undoes the block.
- Working hours 09:00 to 17:30, Europe/London. No lunch hour between 12:30 and
  13:30.
- 15 minutes clear either side of an existing meeting. Back to back slots read
  as available and are not.
- Nothing inside the next 24 hours. By the time the user reads the draft and
  sends it, a slot tomorrow morning may be gone.
- Duration comes from the request. Where none is stated, 30 minutes.
- Four slots at most, across at least two different days. A list of six reads as
  an empty diary, which is not the impression the user wants to give.
- Prefer days that are not already heavy. Where there is a choice, avoid a day
  with more than six hours already booked.

If there are fewer than two slots in the next fortnight, do not stretch further
out to fill the list. Draft a shorter reply offering what there is and say in the
run output that the diary is full, because that is a thing the user needs to know
independently of this email.

## Two kinds of reply

**They asked for times.** Offer the slots. Plain list, one per line, day and
date and time. Add the date the calendar was checked so the recipient knows the
list has an age, and one line saying the user can work to other times if none
suit.

**They proposed times.** Answer their proposal first, before offering anything.
Say yes to the earliest one that is genuinely free, or say none of those work
and then offer alternatives. A reply that ignores the times somebody suggested
and lists four different ones reads as rude, and it is the most common way this
kind of automation annoys people.

## The draft

Correspondence voice from `config.md`. Reply draft into the existing thread with
`outlook_create_reply_draft`, never a new message.

External example:

```
Hi Priya,

Good to hear from you. Happy to find a time.

I have these free at the moment, as of this morning:

Tuesday 14 October, 10:00 or 14:30
Wednesday 15 October, 11:00
Thursday 16 October, 09:30

Any of those any good for you please? If none of them work I can look further
out, just say.

Thanks,
Karl

Karl Wakley
Head of Product, Rethink Demand
rethinkdemand.com
```

Internal is shorter. No warm opener, no signature block, just the times and a
question.

```
Hi Sam,

Free Tuesday 10:00 or 14:30, or Wednesday 11:00. Any of those work?

Thanks,
Karl
```

## What goes in the run output

Three short lists, nothing else.

**Drafted.** One line each: who it is to, what they asked for, and the slots
offered. The user should be able to check the whole run without opening Outlook.

**Not drafted, worth a look.** The ambiguous ones, one line each with the reason.

**Nothing found.** If there were no requests at all, that is the entire output.
One line. This runs ten times a day and most runs will find nothing, so an empty
run has to be silent or people turn it off in a fortnight.

Do not report the skipped duplicates. They are noise.

## Hard limits

- Never send.
- Never create a calendar event, a hold, or a placeholder.
- Never accept or decline an invite.
- Never offer a slot the calendar shows as tentative, blocked or out of office.
- Never offer a slot that is only free because you ignored the buffer rule.
- Where the sender is in another timezone, give the times in London and offer to
  work to theirs. Do not convert unless their timezone is stated.
