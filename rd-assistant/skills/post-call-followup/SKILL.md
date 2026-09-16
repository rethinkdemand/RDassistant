---
name: post-call-followup
description: Turn notes or a transcript from a call into a recap email draft in Outlook plus an action list with owners and dates. Use when the user says "I just got off a call", "follow up on this call", "write up my notes", "turn this transcript into a recap", or pastes call notes and asks what to do with them. Run on demand, not on a schedule. Creates an Outlook draft. Sends nothing.
---

# Post-call follow-up

Read `../../config.md` first, then `../day-debrief/references/recap-email.md` for
the recap shape and voice.

The user has just finished a call and has ten minutes before the next one. Do not
interview them. Work from what they gave you, ask at most two questions, and
produce the draft.

## Input

Whatever they hand over: pasted notes, a Teams transcript, a recording summary, a
photo of a notepad, or four bullet points. Work with what arrives.

If the input is too thin to identify who was on the call or what was agreed, say
which of the two is missing and ask for it. One question, not a form.

## Steps

### 1. Identify the call

Search the calendar for the meeting, most likely in the last few hours. That
gives you the attendee list, the invite body and the organisation, which the
notes usually do not.

If no matching calendar entry exists, work from the notes and say in the output
that the attendee list came from the notes rather than from the invite, so the
user checks it before sending.

### 2. Pull the history

Search mail and Teams with those attendees, last 60 days. You need this for two
reasons: to write a reply draft into the existing thread rather than starting a
new one, and to catch an action from a previous call that was repeated in this
one. An action raised twice is the one that matters.

### 3. Separate what was said from what was decided

Go through the notes and sort every item into one of three buckets:

- **Decided.** Somebody said it would happen.
- **Discussed.** Talked about, not resolved.
- **Raised.** Mentioned once, nobody picked it up.

Only the first bucket produces actions. The second goes into the recap body as
open. The third gets listed in the run output for the user, not in the email,
because a half heard point in a recap email starts an argument.

### 4. Build the action list

A table in the run output. Not in the email, which uses the plain list from the
recap reference.

| Action | Owner | By when | Source |
| --- | --- | --- | --- |

Rules for the columns:

- **Owner** is a person who was on the call. If ownership was not stated, write
  "not assigned" and leave it. Do not assign work to someone who did not accept
  it, including the user.
- **By when** is a date somebody actually said. If no date was agreed, write "no
  date agreed" and, in a separate line under the table, propose one with a
  reason. Keep the proposal out of the table so it never reads as agreed.
- **Source** is the line in the notes it came from. This is what the user checks
  against in twenty seconds.

### 5. Write the draft

Create the recap draft in Outlook. Reply draft into the existing thread where one
exists, new draft where it does not.

Then show the user, in the run output:

1. The action table.
2. The draft body in full, so they can read it without opening Outlook.
3. One line confirming where the draft was created and who it is addressed to.
4. Anything in the "raised" bucket, under a short heading, as items they may want
   to pick up separately.

### 6. Offer one revision

Ask whether they want the draft changed, in one line. If they do, update the
draft in Outlook and confirm which one changed. Do not rewrite the action table
unless they ask.

## Rules specific to this skill

- Nothing sends. Ever. The draft sits in Outlook.
- No figures in the draft, per `config.md`, even when pricing was the point of
  the call. "We agreed to come back to the commercials next week" is the line.
- Do not add an action that the user should take but nobody mentioned. If you
  think one is missing, put it in the run output under a line saying it was not
  raised on the call, and leave it out of the email.
- Do not smooth over a disagreement. If the notes show two people wanted
  different things and it was not resolved, the recap says it is open.
- If the call was internal, the recap is four lines and the actions. No warm
  opener, no soft question.
