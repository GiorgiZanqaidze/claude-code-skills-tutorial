# Solution 1 — Skill with `blocked` status

Replace the status table and behavior section of `.claude/skills/todo-formatter/SKILL.md`
with the following. Also update the frontmatter `description` to mention blocking, so the
model triggers on phrases like "blocked on" or "park this".

```markdown
---
name: todo-formatter
description: Use whenever the user wants to add, edit, normalize, or mark blocked a TODO entry in todos.md. Enforces a consistent line format with priority, status, and ISO date. Trigger on phrases like "add a todo", "mark X done", "blocked on", "park this", "log this as a todo".
---

# todo-formatter

Append or edit entries in `todos.md` using exactly this line format:

    - [STATUS] (PRIORITY) YYYY-MM-DD — description

## Field rules

| Field    | Allowed values                                                       | Notes |
|----------|----------------------------------------------------------------------|-------|
| STATUS   | ` ` (open), `x` (done), `~` (in progress), `!` (blocked)             | Single char in brackets |
| PRIORITY | `high`, `med`, `low`                                                 | Lowercase |
| Date     | YYYY-MM-DD                                                           | Today when adding; preserve when editing |
| Desc     | Free text, one line                                                  | No trailing punctuation |

## Examples

    - [ ] (high) 2026-05-25 — write quarterly report
    - [~] (med)  2026-05-24 — refactor auth middleware
    - [!] (high) 2026-05-25 — ship release (blocked: waiting on legal review)
    - [x] (low)  2026-05-20 — clean up old branches

## Behavior

1. **Adding** — append a new line, preserve order of existing entries.
2. **Marking done** — change only the status character.
3. **Editing priority** — change only the priority token.
4. **Marking blocked** — set status to `!` and append the blocker reason as a parenthetical
   at the end: `(blocked: <reason>)`.
5. **Unblocking** — set status back to ` ` (or `~` if work resumes) and remove the
   `(blocked: ...)` parenthetical.
6. **Unknown priority** — default to `med` and say so in your reply.

Never wrap the file in code fences. Never add a header.
```

## Why the description change matters

The model decides whether to invoke the skill by reading the `description` field. If
"blocked" never appears there, the model may not recognize "this is blocked on legal" as
something the skill handles, and might write the line in some other format.
