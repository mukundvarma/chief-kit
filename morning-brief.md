# morning-brief — daily digest

Spec for the scheduled task that delivers a short daily brief from the chief system. Optional, and independent of `refresh-meetings` — it reads the boards but does not modify them. Recreate it with the `schedule` skill / scheduled-task tools, pointed at the user's own `MEETINGS.md` and `TASKS.md`.

## Schedule

- Cron: `15 6 * * *` (every morning, shortly after `refresh-meetings` so the boards are current).
- Runs in a fresh, non-interactive session.

## What it does each run

1. Read the user's `MEETINGS.md` and `TASKS.md`.
2. Produce a short, scannable brief with three sections. No preamble or sign-off.

### Today's meetings

From `MEETINGS.md`, list cards in the **Upcoming Meetings** and **Appointments** columns scheduled for today (use today's date). For each meeting show time, title, and invitees/attendees (if fewer than 10; omit the list if 10 or more). If none, say "No meetings today."

### Tomorrow's meetings

Show meetings for the next calendar day AND the next business day (if different). For example, on a Friday show both Saturday and Monday; on other weekdays just show the next day. Use the same format as today's section (time, title, invitees if < 10). Label each sub-section with the date (e.g. "Saturday Jul 18" / "Monday Jul 20"). If none, say "No meetings."

### Priority tasks

From `TASKS.md`, find cards (lines starting with `- [ ]`) tagged `#important` and/or `#urgent`, grouped into three buckets:

- **Do now** — both `#important` and `#urgent`; list first.
- **Important** — `#important` only.
- **Urgent** — `#urgent` only.

For each, show the card text and its column (category). If none are tagged, say "No priority-tagged tasks."

## Notes

- **Read-only.** This task never edits the boards; it only surfaces what is already there. Board upkeep is `refresh-meetings`' job.
- Order it after `refresh-meetings` (a few minutes later) so the meetings section reflects the freshly synced calendar.
- The brief is delivered in the task's run output. Optionally render it as a styled HTML artifact if you want a nicer view on desktop.
