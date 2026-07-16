# Connectors

## How tool references work

Plugin files use `~~category` as a placeholder for whatever tool the user connects in that category. The plugin is tool-agnostic — it describes workflows in terms of categories rather than specific products, so anyone can use it with the calendar they already have.

## Connectors for this plugin

| Category | Placeholder  | Options                              |
| -------- | ------------ | ------------------------------------ |
| Calendar | `~~calendar` | Google Calendar, Microsoft 365 / Outlook |

The calendar connector is optional and only needed if the user wants meeting tracking (the `refresh-meetings` and `morning-brief` automations). Read-only access is the recommended default; grant write access only if the user wants Chief to create events.
