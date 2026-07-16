# Customization

Chief ships with sensible defaults, but most pieces can be swapped. These are pointers, not instructions — ask Claude to set any of them up.

## Sync

- Use **Obsidian Sync** instead of iCloud for cross-device sync that works off the Apple ecosystem.
- Use the **Obsidian Git** plugin to version and back up the vault to GitHub/GitLab.
- Point the `chief/` folder at Dropbox, Google Drive, or OneDrive if that's where you already live.

## Calendar

- Swap Google Calendar for **Microsoft 365 / Outlook** — the meeting sync works the same way.
- Track **multiple calendars** (personal + work + shared team) and merge them into one board.
- Tune the exclusion filters in `CLAUDE.md` to hide (or keep) whatever recurring noise you want.
- Change the refresh time or cadence (e.g. twice daily, or weekdays only) in the `refresh-meetings` task.
- Grant **write access** to let Chief create and edit calendar events, not just read them.

## Meetings

- Let Chief **book meetings for you** by giving the calendar connector write scope, then just ask it to schedule.
- Have Chief **draft invites or agendas** into a note before you send them.
- Add a **Done / Past** column to `MEETINGS.md` if you want a record of what happened.

## Tasks and priorities

- Rename or re-order the **category columns** in `TASKS.md` to match your work.
- Add your own **priority tags** beyond `#important` / `#urgent` and reflect them in `PRIORITIES.md`.
- Add columns like **Someday** or **Waiting On** for a lightweight GTD flow.
- Drop the Dataview `PRIORITIES.md` view entirely if you prefer to triage by hand.

## Briefings and automation

- Reschedule or reshape the **morning brief** (e.g. add weather, top emails, or a weekly Friday recap).
- Add an **evening wrap-up** task that logs what got done and rolls incomplete items forward.
- Have the brief delivered as a **styled HTML artifact** or pushed somewhere you'll see it.

## Interface

- Add other **connectors** (Slack, email, project trackers) so Chief pulls tasks and context from where your work actually happens.
- Use **Dispatch** to talk to Chief from your phone while Obsidian stays the viewing surface.
- Extend `CLAUDE.md` with more **memory** (people, projects, glossary) so Chief acts more like a colleague who knows your world.
