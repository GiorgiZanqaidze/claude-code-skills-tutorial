# Module 11 — Skills, Agents, Hooks & Settings

A hands-on mini-project that demonstrates **the four core extensibility mechanisms** in Claude Code, all wired into one tiny project: a TODO list manager.

## What you'll learn

| Concept | What it is | Demo file |
|---------|-----------|-----------|
| **Skill** | Reusable, model-invoked instructions packaged with optional scripts/resources | `.claude/skills/todo-formatter/SKILL.md` |
| **Subagent** | A specialized assistant with its own system prompt and restricted toolset | `.claude/agents/todo-prioritizer.md` |
| **Hook** | Shell command the harness runs automatically on lifecycle events | `.claude/settings.json` (`hooks` key) |
| **Settings** | Project config: permissions, env vars, hooks, model | `.claude/settings.json` |

The TODO list lives in [`todos.md`](./todos.md). Everything else exists to manipulate or guard it.

---

## How the pieces fit together

```
You ask Claude to add a todo
        │
        ▼
┌───────────────────────────┐
│ Skill: todo-formatter     │  ← model decides to invoke it based on the description
│  - normalizes priority    │
│  - enforces format        │
└───────────┬───────────────┘
            │ edits todos.md
            ▼
┌───────────────────────────┐
│ Hook: PostToolUse         │  ← harness runs this automatically after the Edit
│  - logs the change        │
└───────────────────────────┘

You ask "what should I work on first?"
        │
        ▼
┌───────────────────────────┐
│ Subagent: todo-prioritizer│  ← spawned via the Agent tool, has read-only tools
│  - returns ranked list    │
└───────────────────────────┘

All of the above is gated by:
┌───────────────────────────┐
│ Settings: permissions     │  ← e.g. auto-allow Read on todos.md, deny network
└───────────────────────────┘
```

---

## Walkthrough

### 1. Settings (`.claude/settings.json`)

Project-level configuration. This file:
- **Permissions** — auto-allows `Read` and `Edit` on `todos.md` so the user isn't prompted
- **Env vars** — sets `TODO_FILE=todos.md` so hooks and skills can find the file
- **Hooks** — registers a `PostToolUse` hook that logs every edit to `todos.md`

### 2. Skill (`.claude/skills/todo-formatter/SKILL.md`)

A skill is a directory with a `SKILL.md` file that has YAML frontmatter (`name`, `description`).
The model reads the description, decides when it's relevant, and follows the instructions inside.

Try it:
```
> add "buy milk" as a high priority todo
```
Claude sees the request matches the skill's description, follows the format rules, and appends a properly formatted entry to `todos.md`.

### 3. Subagent (`.claude/agents/todo-prioritizer.md`)

A subagent is a separate Claude conversation with its own system prompt and a restricted toolset.
The main Claude invokes it via the `Agent` tool when it needs an independent opinion or a parallel task.

Try it:
```
> use the todo-prioritizer agent to rank my todos
```

### 4. Hook (in `.claude/settings.json`)

A hook is a shell command the harness runs on lifecycle events (`PreToolUse`, `PostToolUse`, `UserPromptSubmit`, `Stop`, etc.).
The one here writes a one-line entry to `audit.log` every time `todos.md` is edited.

---

## Exercises

See [`exercises/`](./exercises/) — four short tasks, one per concept.
Reference answers are in [`solutions/`](./solutions/).

## Trying it locally

1. `cd 11-skills-agents-hooks-settings`
2. Run `claude` from inside this folder so the project-scoped `.claude/` is picked up
3. Approve any prompts on first run (Claude will ask before executing the hook command)
4. Try: *"add 'write report' as a medium-priority todo"*, then *"use the todo-prioritizer agent to rank everything"*

> **Heads up:** The hook in this demo writes to `audit.log` using PowerShell on Windows. If you're on macOS/Linux, swap the command in `settings.json` to the bash equivalent shown in [`solutions/hook-bash.md`](./solutions/hook-bash.md).
