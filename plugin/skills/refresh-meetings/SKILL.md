---
name: refresh-meetings
description: >
  Create the daily scheduled task that syncs a Chief user's MEETINGS.md Kanban
  board from their calendar. Use when setting up Chief meeting automation, when
  the user asks to "set up the morning meeting refresh", "sync my calendar to
  chief daily", or to recreate the refresh-meetings task.
---

# Set up the meeting refresh task

Create a scheduled task that keeps the user's `MEETINGS.md` current from their `~~calendar` connector. Only do this if the user opted into meeting tracking and has authorized the connector.

## Schedule

- Cron: `0 6 * * *` (every morning, 6:00 in the user's home timezone).
- Runs in a fresh, non-interactive session.

## What the task should do each run

1. Pull the next ~14 days from the calendars the user chose to track.
2. Apply the user's exclusion filters (e.g. recurring standups, focus/blocked time, all-day events, personal errands).
3. Rewrite only the **Upcoming Meetings** and **Appointments** columns of `MEETINGS.md`.
4. Never touch the **To Schedule** column; it is hand-maintained.
5. Preserve the `kanban-plugin` frontmatter and the `%% kanban:settings %%` block.
6. Show times in the user's home timezone; append a second zone for out-of-town events (e.g. `4:00pm PT (7:00pm ET)`).
7. Check `CLAUDE.md` for onboarding gaps (empty People table, sparse Projects, thin glossary, blank company.md). If any are found, write `onboarding-gaps.md` into the chief folder so the next interactive session can prompt the user.

## Requirements

- **Read-only calendar.** The task proposes bookings; the user creates the events. Do not request write access unless the user asks.
- **Persistent folder grant.** The unattended run needs a standing grant to the `chief` folder, or it falls back to dropping a dated report note instead of updating the board. After creating the task, have the user click "Run now" once to pre-approve folder + connector access.

Create the task with the scheduling tools, embedding the steps above as its prompt and pointing it at the user's `MEETINGS.md`.
