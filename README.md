# Chief — a plain-Markdown chief-of-staff kit

Chief is a single-interface, low-maintenance command center where Claude acts as your chief of staff. You talk to Claude; Claude maintains the files. Everything is plain Markdown living in your own storage, viewed in Obsidian on Mac and iPhone. No hosted account, no lock-in, works offline, and you do near-zero project-management upkeep.

This repo is a reusable kit for setting the system up for yourself. It contains the install flow, the design rationale, blank templates, and the optional calendar-sync spec.

## What's in the box

- `STARTUP.md` — the setup flow. Point Claude at this file in a Cowork chat and it walks you through building your own `chief/` folder.
- `DESIGN_PHILOSOPHY.md` — what the system is and, more importantly, why it's built this way. Read this to understand the intent before changing anything.
- `templates/` — blank, placeholder-only versions of every file the system uses:
  - `Home.md` — landing note that links everything.
  - `TASKS.md` — Obsidian Kanban board. Columns = categories, cards = projects, checklists = tasks.
  - `MEETINGS.md` — Obsidian Kanban board (Upcoming Meetings, Appointments, To Schedule).
  - `PRIORITIES.md` — Dataview note rendering an Eisenhower matrix computed from `TASKS.md`.
  - `CLAUDE.md` — working memory (identity, people, terms, projects, preferences, conventions).
  - `memory/` — deeper knowledge base scaffold (`glossary.md`, `context/company.md`).
- `refresh-meetings.md` — spec for the optional daily 6am calendar sync.
- `morning-brief.md` — spec for the optional daily digest (today's meetings + priority tasks).
- `CUSTOMIZATION.md` — ways to set things up differently (sync, calendar, meetings, briefings).
- `LICENSE` — MIT.

## Prerequisites

- **Obsidian**, with two community plugins enabled: **Kanban** (renders the boards) and **Dataview** (renders the priorities view). Settings > Community plugins.
- **Claude in Cowork mode** — the setup flow uses Claude to stamp out and maintain your files.
- **Optional:** a calendar connector (Google Calendar or Microsoft 365, read-only) if you want meeting tracking.

## Setup

1. Clone or download this repo somewhere Claude can reach it.
2. Open a Cowork chat and tell Claude: *"Set up the Chief system for me — follow STARTUP.md in this folder."*
3. Answer the setup questions (identity, categories, whether to track meetings). Claude copies the templates into a `chief/` folder in your Obsidian vault, substituting your values.
4. Open the vault in Obsidian on Mac and iPhone, enable the Kanban and Dataview plugins, and you're running.

## Design rules (don't break these)

- **One interface.** Obsidian is the sole surface. Don't build a second dashboard.
- **Plain Markdown you own.** No GitHub/Notion/Trello sync unless you explicitly want it.
- **Claude maintains, you read.** Adding tasks and meetings happens by asking Claude; direct editing in Obsidian is the fallback.
- **Calendar read-only by default.** Claude proposes bookings; you create the events.

See `DESIGN_PHILOSOPHY.md` for the full reasoning and the list of approaches that were tried and deliberately rejected.
