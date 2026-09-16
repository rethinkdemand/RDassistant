---
name: todays-briefings
description: One short briefing per external meeting today. The last email and Teams exchanges with the people in the room, the agenda or invite topic, what is still open with them, and three things to raise. Use when the user says "brief me for today", "what are my meetings today", "prep for my calls", or when a scheduled task calls this skill. Reads Outlook and Teams for that user only. Creates no drafts and sends nothing.
---

# Today's briefings

Read `../../config.md` first.

Runs at 08:00. The reader is on a train or making toast. One screen per meeting,
no more.

## Scope

External meetings only. An external meeting is one with at least one attendee
whose email domain is not RD's.

Internal meetings get a single line at the top: how many there are and when. No
briefing for them.

If there are no external meetings today, the whole output is one line saying so,
plus the internal line. Do not produce a briefing about nothing. A person who
gets two empty briefings stops opening the third.

## What to read, per meeting

For each external meeting, take the external attendees and search:

1. **Mail with those people, last 60 days.** Both directions. Read the most
   recent thread in full and skim the rest.
2. **Teams messages with those people, last 60 days.** Chats and any shared
   channel.
3. **The invite itself.** Body, subject, attachments, and who organised it.
4. **Mail inside RD about this meeting or these people, last 14 days.** A
   colleague may have moved something the user has not seen.

## What to produce, per meeting

A heading with the time, the meeting title and the organisation. Then:

**In the room.** Each external attendee: name, role if it is known, and one
clause on where they sit in the conversation. Name RD colleagues who are also
attending, without roles.

**Why it is happening.** One or two sentences from the invite and the thread that
led to it. If the invite has no body and no thread explains it, say the purpose
is not stated anywhere you can see. That is worth knowing before the call.

**Last contact.** The most recent exchange: date, channel, who wrote last, and
what it said in one sentence. If the user owes a reply, say so here.

**Still open.** Anything asked for and not answered, promised and not delivered,
or agreed and not done, in either direction. Give the date each item started.
If nothing is open, write "Nothing open".

**Three to raise.** Three items, each tied to something above. Format each as the
question or point itself, in the words the user could say, then in brackets where
it came from.

Grounding rule for this section, and it is the one that decides whether people
trust the briefing: every one of the three traces to a specific email, message
or invite. If there is only material for two, give two and say the third would
be invented. Never round up to three with generic advice about building
rapport or confirming next steps.

## Rules specific to this skill

- Create no drafts. This skill produces output only.
- No figures. If the thread is about pricing, write "the commercials from the
  4 June thread" and let the user open it.
- Keep each briefing to what fits on a phone screen. If a meeting has a long
  history, the briefing gets shorter, not longer: the user does not need the
  history, they need the last state of it.
- Order the briefings by meeting time, earliest first.
- A meeting the user organised and a meeting the user was invited to are
  different situations. Say which it is in the heading if it is not obvious.
