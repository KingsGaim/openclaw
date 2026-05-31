---
name: local-file-tools
description: "Read, write, edit, search, and manage local files and directories on the workspace."
---

# Local File Tools

Read, write, edit, and manage files/directories in the local workspace.

## Available Tools

### read
- Read text files or images (jpg, png, gif, webp)
- Supports `offset` (line number) and `limit` (max lines) for large files
- First 2000 lines or 50KB truncated by default
- Images sent as attachments

### write
- Create new file or overwrite existing
- Auto-creates parent directories
- Parameters: `path`, `content`

### edit
- Targeted text replacement in existing files
- Each `oldText` must match a unique, non-overlapping region
- Merge nearby changes into single edit to avoid overlap
- Parameters: `path`, `edits: [{oldText, newText}]`

### exec
- Run shell commands
- Background continuation for long-running work
- Use `process` tool to manage running sessions

## Best Practices

- Use `offset`/`limit` for large files instead of reading all at once
- When editing, read first to find exact text to replace
- `trash` > `rm` for recoverable deletes
- Always verify file exists before editing
- Create parent dirs automatically with `write`

## Common Patterns

```bash
# List files
ls -la /path/

# Find files
find . -name "*.py" -type f

# Read large file in parts
read path=large.txt offset=1 limit=100   # lines 1-100
read path=large.txt offset=101 limit=100 # lines 101-200
```
