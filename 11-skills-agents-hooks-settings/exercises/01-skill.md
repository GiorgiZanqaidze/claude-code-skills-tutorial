# Exercise 1 — Extend the `todo-formatter` skill

The current skill in `.claude/skills/todo-formatter/SKILL.md` supports three statuses:
` ` (open), `x` (done), `~` (in progress).

## Your task

Add a fourth status `!` meaning **blocked**, and teach the skill to use it when the user says
something like "this is blocked on the design review" or "park this until next week".

## Requirements

1. Update the status table in `SKILL.md`.
2. Add at least one example line showing a blocked todo.
3. Add a behavior rule: when the user says a task is blocked, the skill should write the
   reason as a parenthetical at the end of the description, Ve.g.
   `- [!] (high) 2026-05-25 — ship release (blocked: waiting on legal review)`.

## How to verify

After editing, start `claude` in this folder and try:

```
> mark the analytics schema todo as blocked on the data team
```

The skill should rewrite that line with status `!` and the parenthetical reason.

## Hints

- Skills are *instructions for the model*, not code. You're editing prose, not JSON.
- The frontmatter `description` is what the model uses to decide when to invoke the skill —
  consider whether you need to mention "blocked" there too so the model triggers on
  blocker-related phrases.
