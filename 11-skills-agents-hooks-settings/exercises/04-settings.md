# Exercise 4 — Tighten permissions in `settings.json`

The starter `settings.json` is permissive about PowerShell:

```json
"allow": [
  "Read(todos.md)",
  "Read(audit.log)",
  "Edit(todos.md)",
  "Bash(powershell:*)"
]
```

`Bash(powershell:*)` auto-approves **any** PowerShell command. For a real project this is
too broad — Claude could run anything from a passing thought without prompting you.

## Your task

Replace the blanket `Bash(powershell:*)` rule with a minimal allowlist of just the
PowerShell commands you actually need in this project, and add a `deny` rule that catches
common destructive operations even if some future rule accidentally allows them.

## Requirements

1. Remove `Bash(powershell:*)` from `allow`.
2. Add specific allow rules for the two commands the hooks need:
   - The `Add-Content -Path audit.log ...` invocation
   - (If you have other harmless reads, allow those too)
3. Add a `deny` rule that blocks `Remove-Item`, `rm -rf`, and `git push --force`
   (so even if you later loosen `allow`, these stay blocked).
4. Verify by starting `claude` and asking it to "run any PowerShell command you like" — it
   should now have to ask you before running anything not on the new allowlist.

## Hints

- Permission rules support glob-ish matching. `Bash(Add-Content*)` matches any command
  starting with `Add-Content`.
- `deny` always wins over `allow`.
- The `permissions` reference lives in the Claude Code docs under "Settings" — use
  `claude --help` or check the docs site for the exact matcher syntax your version
  supports.

## Stretch

Add an `env` entry that sets `CLAUDE_PROJECT_NAME=todo-demo` and reference it from one of
the hook commands using `$env:CLAUDE_PROJECT_NAME`.
