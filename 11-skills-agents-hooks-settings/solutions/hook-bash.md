# Bash equivalents for the demo hooks

If you're on macOS or Linux, swap the PowerShell commands in `.claude/settings.json` for
these bash equivalents.

## `PostToolUse` — audit log on edits to `todos.md`

```json
"PostToolUse": [
  {
    "matcher": "Edit|Write",
    "hooks": [
      {
        "type": "command",
        "command": "f=$(jq -r '.tool_input.file_path' 2>/dev/null); case \"$f\" in *todos.md) echo \"$(date -u +%Y-%m-%dT%H:%M:%SZ) edited todos.md via $(jq -r '.tool_name')\" >> audit.log ;; esac"
      }
    ]
  }
]
```

> Note: this pipes stdin into `jq` twice, which means the input is read twice. A more
> robust version captures stdin once:
>
> ```json
> "command": "p=$(cat); f=$(printf %s \"$p\" | jq -r '.tool_input.file_path'); case \"$f\" in *todos.md) echo \"$(date -u +%Y-%m-%dT%H:%M:%SZ) edited todos.md via $(printf %s \"$p\" | jq -r '.tool_name')\" >> audit.log ;; esac"
> ```

## `UserPromptSubmit` — log every prompt

```json
"UserPromptSubmit": [
  {
    "hooks": [
      {
        "type": "command",
        "command": "echo \"$(date -u +%Y-%m-%dT%H:%M:%SZ) user prompt submitted\" >> audit.log"
      }
    ]
  }
]
```

## Prereqs

- `jq` must be installed (`brew install jq` or `apt install jq`).
- The working directory when the hook runs is the project root, so `audit.log` is created
  there.
