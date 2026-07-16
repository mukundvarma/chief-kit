# Chief — Startup Flow

Paste this file (or point Claude at it) in a fresh Cowork chat to recreate the Chief chief-of-staff system for a new user. Claude: follow these steps in order. Use the `AskUserQuestion` tool for each questionnaire step so the user picks from options instead of typing prose. Read `./DESIGN_PHILOSOPHY.md` first to understand intent, then copy it into the user's `chief/` folder alongside the other files.

## What you're building

A single-interface, plain-Markdown chief-of-staff system the user views in Obsidian (Mac + iPhone) and Claude maintains. Two Kanban boards (tasks, meetings), a memory file, and an optional daily calendar sync. Templates are in `./templates/`.

## Step 0 — Locate or create the vault folder

Ask where the system should live. If the user uses Obsidian, target a `chief/` subfolder inside their vault (usually `~/Library/Mobile Documents/iCloud~md~obsidian/Documents/<Vault>/`). Otherwise offer a plain iCloud/Drive folder. Request access to that folder with `request_cowork_directory`.

## Step 1 — Identity (AskUserQuestion)

Collect, in one or two questions:
- Their name and role (free text via the elicitation form is fine).
- Whether Claude should be their chief of staff for Work only, or Work + Personal.

## Step 2 — Categories (AskUserQuestion)

Offer a default Work category set and let them adjust: Science, Engineering, Management, Funding, Commercialization. Plus a top-level Personal bucket. These become the columns of the task board. Confirm the final list before writing.

## Step 3 — Task board format (AskUserQuestion)

Confirm the hierarchy convention: column = category, card = project, checklist inside a card = tasks. Note that rendering as a board requires the Obsidian Kanban community plugin; tell them to install it (Settings > Community plugins > Kanban).

## Step 4 — Meetings (AskUserQuestion)

Ask whether to set up meeting tracking. If yes:
- Ask which calendar provider (Google Calendar / Microsoft 365). Surface the connector via the registry and have them authorize it (read-only is the recommended default).
- After it's connected, list their calendars and ask which to track.
- Ask what to exclude (journal clubs, recurring lab chores, birthdays, deadlines, etc.).
- Ask their home timezone; show times in that zone with a second zone for out-of-town events.
- Ask whether to schedule a daily morning refresh (default 6am). If yes, create a scheduled task mirroring `refresh-meetings` in this repo, pointed at their `MEETINGS.md`, preserving the To Schedule column.

## Step 5 — Stamp out the files

Copy from `./templates/` into the user's `chief/` folder, substituting their values:
- `Home.md` — landing note.
- `TASKS.md` — Kanban board with their category columns.
- `MEETINGS.md` — Kanban board (Upcoming Meetings, Appointments, To Schedule), or omit if they skipped Step 4.
- `CLAUDE.md` — working memory seeded with their identity, preferences, interface conventions, and meeting rules.
- `memory/` — empty glossary + context scaffold.
- `PRIORITIES.md` — Dataview Eisenhower matrix (copy from `./templates/PRIORITIES.md`).
- `DESIGN_PHILOSOPHY.md` — copy from `./DESIGN_PHILOSOPHY.md`.

## Step 6 — Wrap up

- Tell them to open the vault in Obsidian on Mac and iPhone and enable the Kanban and Dataview community plugins.
- If a calendar was connected, suggest clicking "Run now" on the scheduled task once to pre-approve folder + connector access.
- Recommend scoping folder permissions down to just the `chief` folder.

## Design rules to preserve (do not violate)

- One interface (Obsidian). Do not build a second dashboard.
- Plain Markdown in the user's own storage. Do not push GitHub/Notion/Trello unless the user explicitly asks.
- Claude maintains the files; the user should not have to do PM upkeep.
- Calendar stays read-only unless the user opts into write access.
