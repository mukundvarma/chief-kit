# Privacy Policy

_Last updated: 2026-07-16_

Chief-kit is a plugin that helps you set up and maintain a plain-Markdown chief-of-staff system in your own Obsidian vault. This policy explains what the plugin does and does not do with your data.

## Summary

Chief-kit collects nothing. It runs entirely within your own Claude session and operates on files in storage you control. The plugin and its author do not receive, store, transmit, sell, or have any access to your data.

## What the plugin accesses

- **Your local files.** The plugin reads and writes Markdown files in the `chief/` folder of the Obsidian vault you point it at (tasks, meetings, notes, working memory). These files live in your own storage, typically iCloud Drive.
- **Your calendar (optional).** If you enable meeting tracking, the plugin reads events from a calendar connector you authorize yourself (e.g. Google Calendar or Microsoft 365). Read-only access is the default. This connection is between you and your calendar provider; the plugin author is not a party to it and never sees your calendar data.
- **Scheduled tasks (optional).** If you opt in, the plugin creates local scheduled tasks that refresh your meetings board and produce a morning brief. These run in your own Claude environment.

## What the plugin does not do

- It does not collect analytics, telemetry, or usage data.
- It does not send your files, calendar, or any other content to the author or any third-party server operated by the author.
- It contains no tracking, advertising, or external network calls of its own.

## Third parties

The plugin does not add any third-party data processors. The tools you use it with, such as Obsidian, iCloud (Apple), your calendar provider, and Anthropic's Claude, each handle your data under their own privacy policies. Review those services directly for how they process your data.

## Data retention and control

All data created or edited by the plugin stays in your vault. You can read, edit, export, or delete it at any time using Obsidian or your file system. Uninstalling the plugin does not remove your files; they remain yours.

## Changes

If this policy changes, the updated version will be published in this repository with a new "Last updated" date.

## Contact

Questions about this policy can be raised as an issue on the project repository: https://github.com/mukundvarma/chief-kit
