---
name: save
description: |
  Save the current Context Document to a markdown file.
  Triggered by "/save", "/save [path]" commands.
  Must be used after generating a Context Document with /context or /context fast.
---

# Save Context Document

Save the Context Document from the current conversation as a markdown file.

## Usage

```
/save                          → ./context-{project-name}-{date}.md
/save ./docs/                  → ./docs/context-{project-name}-{date}.md
/save ./docs/myapp-context.md  → ./docs/myapp-context.md
```

## Behavior

1. **Check** if a Context Document exists in the current conversation.
   - If none exists, respond:
     ```
     No Context Document in this session. Run /context or /context fast first.
     ```
2. **Warn** if `[needs confirmation]` items remain:
   ```
   Warning: {N} items still marked [needs confirmation]. Save anyway? (y/n)
   ```
3. **Determine file path**:
   - No argument → `./context-{project-name}-{date}.md` in current directory
   - Directory path (ends with `/`) → `{dir}/context-{project-name}-{date}.md`
   - Full file path → use as-is
4. **Write** the Context Document to the file using the Write tool.
5. **Confirm** the save:
   ```
   Context Document saved to {path}
   ```
