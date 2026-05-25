# Exercise 2 — Build a second subagent: `todo-summarizer`

You already have `todo-prioritizer` that ranks todos. Now write a companion agent that
summarizes the *state* of the list — counts by status, counts by priority, and the oldest
open item.

## Your task

Create `.claude/agents/todo-summarizer.md`.

## Requirements

1. **Frontmatter** with `name`, `description`, and a `tools:` list that contains only `Read`
   (the agent should not be able to edit).
2. **System prompt** that instructs the agent to read `todos.md` and reply in this format:

   ```
   Summary
   - Open:        N
   - In progress: N
   - Done:        N
   - Blocked:     N  (only if exercise 1 is done)

   By priority (open + in progress only)
   - high: N
   - med:  N
   - low:  N

   Oldest open: YYYY-MM-DD — <description>
   ```

3. The agent should refuse to modify `todos.md` (since it has no edit tools, this is
   automatic — but mention it in the prompt as a guardrail).

## How to verify

```
> use the todo-summarizer agent
```

You should get the structured summary above, with the numbers matching the current state of
`todos.md`.

## Hints

- Look at `.claude/agents/todo-prioritizer.md` for the file layout and frontmatter shape.
- Keep the system prompt short and prescriptive. Agents work best when they have one job.
