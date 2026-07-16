# refresh-meetings — daily calendar sync

Spec for the scheduled task that keeps `MEETINGS.md` current. Optional: only set this up if the user opted into meeting tracking during setup (STARTUP.md, Step 4). Recreate it with the `schedule` skill / scheduled-task tools, pointed at the user's own `MEETINGS.md`.

## Schedule

- Cron: `0 6 * * *` (every morning, 6:00 in the user's home timezone).
- Runs in a fresh, non-interactive session.

## What it does each run

1. Pull the next ~14 days from the calendars listed in `CLAUDE.md` under "Meeting tracker."
2. Apply the exclusion filters from `CLAUDE.md` (e.g. journal clubs, recurring lab/wet-bench chores, birthdays, payroll/deadline entries).
3. Rewrite only the **Upcoming Meetings** and **Appointments** columns of `MEETINGS.md`.
4. **Never touch the To Schedule column** — it is hand-maintained by the user.
5. Preserve the `kanban-plugin` frontmatter and the `%% kanban:settings %%` block.
6. Show times in the user's home timezone; append a second zone for out-of-town events (e.g. `4:00pm PT (7:00pm ET)`).
7. Check `CLAUDE.md` for onboarding gaps (empty People table, sparse Projects, thin glossary, blank company.md). If any are found, write `onboarding-gaps.md` into the chief folder so the next interactive session can prompt the user to fill them.

## Requirements and sharp edges

- **Calendar connector, read-only.** The task proposes bookings; the user creates the events. Do not request write access unless the user asks.
- **Persistent folder grant.** The unattended run needs a standing grant to the `chief` folder to write the board. Without it, the task falls back to dropping a dated report note instead of updating `MEETINGS.md`. After creating the task, have the user click "Run now" once to pre-approve folder + connector access.
- Scope folder permissions down to just `chief`.

## Setup pointers

- Google Calendar and Microsoft 365 connectors are both viable; pick whichever the user authorized in Step 4.
- Store the calendar list, exclusion rules, home timezone, and second-zone rule in `CLAUDE.md` under "Meeting tracker" so this task and interactive sessions read the same source of truth.
