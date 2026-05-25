# Solution 4 — Tighter permissions

Replace the `permissions` block in `.claude/settings.json` with this:

```json
"permissions": {
  "allow": [
    "Read(todos.md)",
    "Read(audit.log)",
    "Edit(todos.md)",
    "Bash(powershell -NoProfile -Command \"Add-Content*)",
    "Bash(powershell -NoProfile -Command \"$payload*)"
  ],
  "deny": [
    "Bash(Remove-Item*)",
    "Bash(rm -rf*)",
    "Bash(git push --force*)",
    "Bash(git push -f*)",
    "WebFetch",
    "WebSearch"
  ]
}
```

## Why this is safer

| Before | After |
|--------|-------|
| `Bash(powershell:*)` allows any PowerShell command without prompting | Only the two specific commands the hooks need are auto-allowed |
| No defense against destructive commands | Explicit `deny` rules ensure even mistakes can't `Remove-Item` or `git push --force` |
| `WebFetch` already denied | Same — kept |

## Key rules to remember

1. **`deny` always beats `allow`.** Adding a deny rule is a hard floor; you can't
   accidentally loosen it later by adding a broader allow.
2. **Allow rules are prefix matchers.** `Bash(Add-Content*)` matches any command line
   starting with `Add-Content`. Pin them as narrowly as you can.
3. **Project vs user vs local settings.**
   - `.claude/settings.json` — checked into git, shared with the team
   - `.claude/settings.local.json` — gitignored, your personal overrides
   - `~/.claude/settings.json` — user-level, applies to all projects
   Permissions merge across all three; deny rules from any layer apply.

## Stretch: env var in a hook

Add this to `env`:

```json
"env": {
  "TODO_FILE": "todos.md",
  "AUDIT_LOG": "audit.log",
  "CLAUDE_PROJECT_NAME": "todo-demo"
}
```

Then update the audit hook command to include the project name:

```powershell
Add-Content -Path audit.log -Value ($([DateTime]::UtcNow.ToString('o')) + ' [' + $env:CLAUDE_PROJECT_NAME + '] edited todos.md via ' + $payload.tool_name)
```

Now every audit line is tagged with the project, useful if multiple demos share one log.
