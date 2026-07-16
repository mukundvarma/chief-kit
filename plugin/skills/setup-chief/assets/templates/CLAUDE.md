# Memory

## Me
<Name> (<email>), <role>.

## People
| Who | Role |
|-----|------|

## Terms
| Term | Meaning |
|------|---------|

## Projects
| Name | What |
|------|------|

## Preferences
- <communication preferences, e.g. concise; no emojis; cite sources>
- <e.g. no code unless asked>

## Interface / files
- Sole interface: Obsidian vault at chief/ (iCloud), on Mac + iPhone. No separate dashboard. Do not reintroduce GitHub/Notion/Trello unless asked.
- TASKS.md is an Obsidian Kanban board. Columns = categories. Convention: card = project, checklist inside card = tasks.
- MEETINGS.md is an Obsidian Kanban board. Columns = Upcoming Meetings, Appointments, To Schedule. Cards = individual meetings/appointments.
- When editing either, preserve the kanban-plugin frontmatter and the %% kanban:settings %% block.
- Home.md is the vault landing note.
- PRIORITIES.md is a Dataview query note showing an Eisenhower matrix view of tasks. It is read-only (computed from TASKS.md); never edit it directly.
- Priority tags go on cards (projects) in TASKS.md, not on individual checklist items. Use `#important`, `#urgent`, or both. Use `#drop` to mark cards for elimination. Untagged cards are untriaged and only appear in TASKS.md.

## Onboarding checks

On every new interactive session (not scheduled tasks), Claude should scan CLAUDE.md for gaps in core components and use AskUserQuestion to fill them. Run checks in order; stop after the first gap found (one flow per session, not a barrage).

### Trigger
At session start, check if `onboarding-gaps.md` exists in the chief folder. If it does, read it and run the checks below for the listed gaps. If it doesn't exist, still scan CLAUDE.md directly for gaps. Either way, stop after the first gap found.

### Check 1: People table
If the People table has no rows (only the header), ask:
- Question: "Your People table is empty. Want to add key collaborators now?"
- Options: "Yes, let's add people" / "Skip for now"
- If yes: follow up with "Name and role of someone you work with frequently?" (free text via Other). Repeat until the user says done. Add each to the People table.

### Check 2: Projects table
If the Projects table has fewer than 2 confirmed entries (entries with "unconfirmed" or only 1 row), ask:
- Question: "Your Projects table is sparse. Want to flesh it out?"
- Options: "Yes, let's add projects" / "Skip for now"
- If yes: ask "Name and one-line description of an active project?" Repeat until done. For any existing unconfirmed entries, ask the user to confirm or correct them.

### Check 3: Terms / glossary
If the Terms table has fewer than 3 rows, ask:
- Question: "Want to add acronyms or shorthand your team uses so I can decode them?"
- Options: "Yes, let's add terms" / "Skip for now"
- If yes: ask "Term and meaning?" Repeat until done. Also add to memory/glossary.md.

### Check 4: Memory stubs
Read memory/context/company.md. If it contains only template placeholder text (or is under 3 lines of real content), ask:
- Question: "Your org context file is mostly blank. Want to fill in basics about your team/org?"
- Options: "Yes, let's fill it in" / "Skip for now"
- If yes: ask about org name, team size, domain, key tools/platforms. Write answers to memory/context/company.md.

### Skip behavior
If the user says "Skip for now" to any check, do not ask about that same check again in the same session. The check will re-trigger next session until the gap is filled. Once a component has enough content (People >= 1 row, Projects >= 2 confirmed, Terms >= 3, company.md >= 3 lines), that check retires permanently.

## Meeting tracker
- Calendars to pull: <list>
- Exclude from Meetings: <e.g. journal clubs, recurring chores, birthdays, deadlines>
- Appointments column holds personal appointments and social events, separate from work meetings
- Show times in <home TZ>; add a second zone for out-of-town events
- To Schedule column is hand-maintained; never overwrite it on a calendar refresh
