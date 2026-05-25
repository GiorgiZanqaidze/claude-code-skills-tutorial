# Solution 3 — `PreToolUse` quiet-hours guard

Add the following block to the `hooks` object in `.claude/settings.json`, alongside the
existing `PostToolUse` entry.

```json
"PreToolUse": [
  {
    "matcher": "Edit|Write",
    "hooks": [
      {
        "type": "command",
        "command": "powershell -NoProfile -Command \"$p = $input | Out-String | ConvertFrom-Json; if ($p.tool_input.file_path -notmatch 'todos\\.md$') { exit 0 }; $h = [int](Get-Date -Format HH); if ($h -ge 22 -or $h -lt 6) { [Console]::Error.WriteLine('Blocked: no edits to todos.md between 22:00 and 06:00 local time.'); exit 2 } else { exit 0 }\""
      }
    ]
  }
]
```

## How it works

| Exit code | Effect on a `PreToolUse` hook |
|-----------|-------------------------------|
| `0`       | Allow the tool call           |
| `2`       | Deny it; stderr is shown to the model |
| other     | Non-blocking error            |

The hook:

1. Reads the JSON payload from stdin (`$input` in PowerShell).
2. Bails out early with `exit 0` if the file path isn't `todos.md` — we only care about
   that one file.
3. Reads the current hour. If it's late, prints a message to **stderr** and exits with
   code 2. The model sees that stderr message and will tell you it couldn't make the edit.
4. Otherwise allows the edit through.

## Testing without waiting until 10pm

Temporarily force the block by changing the condition to `if ($true)`. Run a request, see
the denial, then revert. Or run the command manually with a synthetic payload:

```powershell
'{"tool_name":"Edit","tool_input":{"file_path":"todos.md"}}' |
  powershell -NoProfile -Command "<paste the command body here>"
```

and check `$LASTEXITCODE`.

## Bash equivalent

For macOS/Linux, swap the command for:

```json
"command": "f=$(jq -r '.tool_input.file_path' 2>/dev/null); case \"$f\" in *todos.md) h=$(date +%H); if [ \"$h\" -ge 22 ] || [ \"$h\" -lt 6 ]; then echo 'Blocked: no edits to todos.md between 22:00 and 06:00.' >&2; exit 2; fi ;; esac; exit 0"
```
