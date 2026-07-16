---
name: morning-brief
description: >
  Create the daily scheduled task that delivers a Chief user a short morning
  brief of today's meetings and priority-tagged tasks. Use when setting up Chief
  automation, or when the user asks to "set up a morning brief", "give me a daily
  digest from chief", or to recreate the morning-brief task.
---

# Set up the morning brief task

Create a scheduled task that delivers a short daily brief from the user's Chief system. It reads the boards but never modifies them, so it is independent of `refresh-meetings`.

## Schedule

- Cron: `15 6 * * *` (every morning, shortly after `refresh-meetings` so the boards are current).
- Runs in a fresh, non-interactive session.

## What the task should do each run

1. Read the user's `MEETINGS.md` and `TASKS.md`.
2. Produce a short, scannable brief with two sections. No preamble or sign-off.

### Today's meetings

From `MEETINGS.md`, list cards in the **Upcoming Meetings** and **Appointments** columns scheduled for today (use today's date). Show each with time and title. If none, say "No meetings today."

### Priority tasks

From `TASKS.md`, find cards (lines starting with `- [ ]`) tagged `#important` and/or `#urgent`, grouped into three buckets:

- **Do now** — both `#important` and `#urgent`; list first.
- **Important** — `#important` only.
- **Urgent** — `#urgent` only.

For each, show the card text and its column (category). If none are tagged, say "No priority-tagged tasks."

## Notes

- **Read-only.** This task never edits the boards; board upkeep is `refresh-meetings`' job.
- Order it after `refresh-meetings` so the meetings section reflects the freshly synced calendar.
- Optionally render the brief as a styled HTML artifact for a nicer desktop view.

Create the task with the scheduling tools, embedding the steps above as its prompt and pointing it at the user's `MEETINGS.md` and `TASKS.md`.
