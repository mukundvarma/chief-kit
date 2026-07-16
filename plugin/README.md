# chief-kit (plugin)

Installs Chief, a plain-Markdown chief-of-staff system in Obsidian that Claude sets up and maintains for you. This is the installable plugin version of [chief-kit](https://github.com/mukundvarma/chief-kit); the repo root also holds the same system as a read-it-yourself kit.

## What it does

Once installed, ask Claude to **"set up chief"** and it walks you through building the system: a task board, a meetings board, a priorities matrix, and working memory, all as plain Markdown in your Obsidian vault. Optional daily automations sync your calendar and deliver a morning brief.

## Skills

- **setup-chief** — the guided install flow. Asks about your identity, categories, and whether to track meetings, then stamps out the files from bundled templates.
- **refresh-meetings** — creates the daily 6am scheduled task that syncs your meetings board from your calendar.
- **morning-brief** — creates the daily digest of today's meetings and priority-tagged tasks.

## Prerequisites

- **Obsidian**, with the **Kanban** and **Dataview** community plugins enabled.
- **Claude in Cowork mode** to run the setup and maintain the files.
- **Optional:** a calendar connector (Google Calendar or Microsoft 365, read-only) for meeting tracking.

## Install

Install from the chief-kit marketplace, then run the setup:

```
/plugin marketplace add mukundvarma/chief-kit
/plugin install chief-kit@chief-kit
```

Then tell Claude: *"set up chief."*
