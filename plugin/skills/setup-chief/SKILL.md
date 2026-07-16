---
name: setup-chief
description: >
  Set up the Chief chief-of-staff system for a user: a plain-Markdown command
  center in Obsidian (task board, meetings board, priorities matrix, working
  memory) that Claude maintains. Use when the user says "set up chief", "install
  chief", "create my chief system", "set up my chief-of-staff", or asks to build
  the Obsidian task/meeting system from this plugin.
---

# Set up Chief

Guide the user through building a Chief chief-of-staff system: a single-interface, plain-Markdown setup they view in Obsidian (Mac + iPhone) and Claude maintains. Two Kanban boards (tasks, meetings), a priorities matrix, working memory, and optional daily calendar automation. Follow the steps in order. Use the `AskUserQuestion` tool for each questionnaire step so the user picks from options instead of typing prose. Read `references/design-philosophy.md` first to internalize intent; copy it into the user's `chief/` folder at the end.

Templates live in `${CLAUDE_PLUGIN_ROOT}/skills/setup-chief/assets/templates/`. Copy from there, substituting the user's values.

## Prerequisites — Obsidian plugins

Chief renders through Obsidian community plugins. Tell the user to install these early (Settings > Community plugins > Browse):

- **Kanban** — required. Renders `TASKS.md` and `MEETINGS.md` as boards.
- **Dataview** — required. Renders the `PRIORITIES.md` Eisenhower matrix.
- **Obsidian Git** — optional. Version and back up the vault to a Git remote.
- **Obsidian Sync** (paid, first-party) — optional. Cross-device sync without relying on iCloud.

## Step 0 — Locate or create the vault folder

Ask where the system should live, branching on the user's setup:

- **Existing Obsidian vault:** target a `chief/` subfolder inside it (usually `~/Library/Mobile Documents/iCloud~md~obsidian/Documents/<Vault>/`).
- **New to Obsidian:** have them download Obsidian, create a new vault (in iCloud Drive if they want Mac + iPhone sync), then create `chief/` inside it. Point Claude at that folder.
- **No Obsidian:** offer a plain iCloud/Drive folder. They keep the Markdown but lose the board and matrix views.

Request access to the chosen folder before writing anything.

## Step 1 — Identity (AskUserQuestion)

Collect, in one or two questions:
- Their name and role (free text is fine).
- Whether Claude should act as chief of staff for Work only, or Work + Personal.

## Step 2 — Categories (AskUserQuestion)

Offer a few preset column bundles and let them adjust; do not assume one domain. Examples:
- **Generic professional:** Projects, Admin, Follow-ups, Meetings.
- **Research / leadership:** Science, Engineering, Management, Funding, Commercialization.
- **Maker / IC:** Building, Reviewing, Planning, Learning.

Add a top-level Personal bucket only if they chose Work + Personal in Step 1. These become the columns of the task board. Confirm the final list before writing.

## Step 3 — Task board format (AskUserQuestion)

Confirm the hierarchy convention: column = category, card = project, checklist inside a card = tasks. Rendering as a board requires the Kanban plugin; confirm it is installed.

## Step 4 — Meetings (AskUserQuestion)

Ask whether to set up meeting tracking. If yes:
- Have them connect a `~~calendar` connector (read-only is the recommended default). **Authorize it before any scheduled task runs** — the connector OAuth must be completed in the user's connector settings first, or the morning tasks fail silently on their first run.
- After it is connected, list their calendars and ask which to track.
- Ask what to exclude (recurring standups, focus/blocked time, all-day events, personal errands, etc.).
- Ask their home timezone; show times in that zone with a second zone for out-of-town events.
- Ask whether to schedule a daily morning refresh (default 6am). If yes, invoke the `refresh-meetings` skill in this plugin to create the scheduled task, pointed at their `MEETINGS.md`.
- Ask whether they also want a daily morning brief. If yes, invoke the `morning-brief` skill in this plugin. Order it a few minutes after the refresh so the boards are current.

## Step 5 — Stamp out the files

Copy from `assets/templates/` into the user's `chief/` folder, substituting their values:
- `Home.md` — landing note.
- `TASKS.md` — Kanban board with their category columns.
- `MEETINGS.md` — Kanban board (Upcoming Meetings, Appointments, To Schedule); omit if they skipped Step 4.
- `CLAUDE.md` — working memory seeded with their identity, preferences, interface conventions, and meeting rules.
- `memory/` — empty glossary + context scaffold.
- `PRIORITIES.md` — Dataview Eisenhower matrix.
- `DESIGN_PHILOSOPHY.md` — copy from `references/design-philosophy.md`.

When editing `TASKS.md` or `MEETINGS.md`, always preserve the `kanban-plugin` frontmatter and the `%% kanban:settings %%` block.

## Step 6 — Wrap up

- Confirm the Kanban and Dataview plugins are enabled so the boards and matrix render.
- If a calendar was connected, confirm the connector is authorized, then have them click "Run now" on the scheduled task once to pre-approve the persistent folder + connector access the unattended runs need.
- Recommend scoping folder permissions down to just the `chief` folder.
- Point them at `references/customization.md` for ways to set things up differently (sync, calendar write access, extra categories, briefings).

## Design rules to preserve (do not violate)

- One interface (Obsidian). Do not build a second dashboard.
- Plain Markdown in the user's own storage. Do not push GitHub/Notion/Trello unless the user explicitly asks.
- Claude maintains the files; the user should not have to do project-management upkeep.
- Calendar stays read-only unless the user opts into write access.
