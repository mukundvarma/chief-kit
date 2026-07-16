# Priorities

Eisenhower view of projects from [[TASKS]]. Tag cards with `#important` and/or `#urgent` in TASKS.md to have them appear here. Untagged cards stay only in the task board.

## Do First (Important + Urgent)

```dataview
TASK FROM "TASKS"
WHERE contains(text, "#important") AND contains(text, "#urgent")
WHERE !completed
```

## Schedule (Important, Not Urgent)

```dataview
TASK FROM "TASKS"
WHERE contains(text, "#important") AND !contains(text, "#urgent")
WHERE !completed
```

## Delegate (Urgent, Not Important)

```dataview
TASK FROM "TASKS"
WHERE contains(text, "#urgent") AND !contains(text, "#important")
WHERE !completed
```

## Drop

```dataview
TASK FROM "TASKS"
WHERE contains(text, "#drop")
WHERE !completed
```
