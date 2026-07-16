# Design Philosophy — Chief

The rationale behind this personal chief-of-staff system. Read this alongside `CLAUDE.md` (the working memory Claude loads automatically) to understand not just what the setup is, but why it is this way.

## Purpose

A single, low-maintenance command center where Claude acts as chief of staff. The user talks to Claude; Claude maintains the files. The user should do near-zero project-management upkeep and never learn a PM tool.

## Principles

1. **Plain Markdown, owned by the user.** Everything is local `.md` files. No hosted account, no lock-in, works offline, full version history via the vault's Git.
2. **One interface.** Obsidian is the sole interface, on Mac and iPhone. No second dashboard to keep in sync. A custom HTML dashboard was built and then deliberately removed to honor this.
3. **Claude maintains, the user reads.** Adding tasks, meetings, or notes happens by asking Claude. Direct editing in Obsidian is always available as a fallback.
4. **Minimal friction over maximal features.** Chosen repeatedly: local files over Notion; Obsidian over a bespoke app; read-only calendar over write access.

## Architecture

Location: `chief/` inside the user's Obsidian vault (iCloud Drive > Obsidian). iCloud syncs it to all Apple devices; no always-on machine required. See `CLAUDE.md` for user identity and vault-specific details.

Files:

- `Home.md` — landing note linking everything.
- `TASKS.md` — Obsidian Kanban board. Columns = categories (Science, Engineering, Management, Funding, Commercialization, Personal). Convention: column = category, card = project, checklist inside a card = tasks. This encodes a three-level hierarchy in a flat board.
- `MEETINGS.md` — Obsidian Kanban board. Columns = Upcoming Meetings, Appointments, To Schedule. Cards = individual meetings. Times in the user's home timezone, with a second zone appended for out-of-town events.
- `CLAUDE.md` — working memory: identity, people, terms, projects, preferences, interface conventions, meeting-tracker rules, onboarding checks. Loaded automatically as project context.
- `memory/` — deeper knowledge base (`glossary.md`, `context/`, `people/`, `projects/`).
- `DESIGN_PHILOSOPHY.md` — this file.
- `fresh_start/` — reusable kit to recreate this system for a new user.

Both boards require the Obsidian Kanban community plugin to render as boards.

`PRIORITIES.md` is a Dataview query note that renders an Eisenhower matrix (Do First, Schedule, Delegate, Drop) from priority tags on checklist items in `TASKS.md`. It is a computed view, never edited directly. Tags (`#important`, `#urgent`, `#drop`) live on cards (project level), not on individual checklist items. Untagged tasks are untriaged and only appear in the task board. Requires the Dataview community plugin.

## Meeting sync

Google Calendar connector (read-only) pulls the calendars listed in `CLAUDE.md` under "Meeting tracker." A scheduled task ("refresh-meetings") runs every morning at 6am, repulls the next 14 days, applies the exclusion filters, rewrites the Upcoming Meetings and Appointments columns while preserving the hand-maintained To Schedule column, and checks for onboarding gaps in `CLAUDE.md` (writing `onboarding-gaps.md` if any are found). Read-only is intentional: Claude proposes bookings; the user creates the events.

## Onboarding

Core components in `CLAUDE.md` (People, Projects, Terms, memory stubs) are checked every morning by the scheduled task and on every interactive session start. Gaps are surfaced via `AskUserQuestion` one at a time until all components are populated. See the "Onboarding checks" section in `CLAUDE.md` for thresholds and flow.

## Decisions made and rejected

- **Rejected: Notion, Trello, GitHub sync.** Evaluated as the cross-device hub; all declined in favor of Markdown-in-iCloud plus Obsidian. Do not reintroduce.
- **Rejected: custom HTML dashboard.** Built, then removed once Obsidian covered laptop and phone. One interface wins.
- **Rejected: Cowork live artifact for meetings.** Built, but live artifacts are desktop-only, so they fail the phone requirement. Superseded by the Obsidian Kanban board.
- **Kept: Dispatch** as the phone path for talking to Claude (control desktop Cowork from the phone), complementary to Obsidian for viewing.

## Open items / sharp edges

- The morning refresh runs in a fresh session and needs a persistent grant to the `chief` folder to write unattended; otherwise it drops a dated report note instead of updating the board.
- Folder permissions should be scoped down to just `chief` (revoke broader iCloud grants).
- Calendar is read-only by design; scheduling still requires the user to book.
