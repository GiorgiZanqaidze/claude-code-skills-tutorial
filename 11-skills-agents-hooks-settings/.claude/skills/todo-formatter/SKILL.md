---
name: todo-formatter
description: Use whenever the user wants to add, edit, or normalize a TODO entry in todos.md. Enforces a consistent line format with priority, status, and ISO date so the file stays grep-friendly. Trigger on phrases like "add a todo", "mark X done", "new task", "log this as a todo".
---

# todo-formatter

Append or edit entries in `todos.md` using exactly this line format:

```
- [STATUS] (PRIORITY) YYYY-MM-DD — description
```

## Field rules

| Field | Allowed values | Notes |
|-------|----------------|-------|
| STATUS | ` ` (open), `x` (done), `~` (in progress) | Single character inside the brackets |
| PRIORITY | `high`, `med`, `low` | Lowercase, no abbreviations like "H" |
| YYYY-MM-DD | ISO date | Use today's date when adding; keep original date when editing |
| description | Free text | One line, no trailing punctuation |

## Examples

```
- [ ] (high) 2026-05-25 — write quarterly report
- [~] (med)  2026-05-24 — refactor auth middleware
- [x] (low)  2026-05-20 — clean up old branches
```

## Behavior

1. **Adding** — read `todos.md`, append the new line at the end, do not reorder existing entries.
2. **Marking done** — change only the status character; keep the original date and priority.
3. **Editing priority** — change only the priority token.
4. **Unknown priority** — if the user doesn't specify one, default to `med` and mention the default in your reply.

Never wrap the file in code fences. Never add a header — `todos.md` is a flat list.
