# Exercise 3 — Add a `PreToolUse` guard hook

The current `settings.json` has a `PostToolUse` hook that logs every edit to `todos.md`.
Your job: add a `PreToolUse` hook that **blocks** edits to `todos.md` between 10pm and 6am
local time (a "no late-night todo edits" guard).

## Your task

Edit `.claude/settings.json` and add a `PreToolUse` entry under `hooks`.

## Requirements

1. Matcher: `Edit|Write`.
2. The hook command should:
   - Read the JSON payload from stdin
   - Check `tool_input.file_path` — if it doesn't end in `todos.md`, exit 0 (allow)
   - If the current hour is `>= 22` or `< 6`, exit with code `2` and print a message to
     stderr explaining the block — Claude Code treats exit code 2 from a `PreToolUse` hook
     as "deny this tool call and show the message to the model".
   - Otherwise exit 0.

## How to verify

1. Temporarily set your system clock forward (or just hardcode the hour check to always
   block while testing).
2. Run `claude` and ask it to add a todo.
3. The edit should be denied and the model should see your error message.

## Hints

- Hook commands run as plain shell commands. On Windows, use
  `powershell -NoProfile -Command "..."`. On macOS/Linux, use bash.
- `Get-Date -Format HH` returns the current hour in PowerShell.
- Exit code semantics for hooks:
  - `0` — allow
  - `2` — block (PreToolUse) or feed stderr back to the model (other events)
  - anything else — non-blocking error

See the existing `PostToolUse` entry for the surrounding JSON shape.
