---
name: update
description: |
  Add or modify sections in an existing Context Document.
  Triggered by "/update" command.
  Must be used after generating a Context Document with /context or /context fast.
---

# Update Context Document

Add or modify content in an existing Context Document.

## Usage

```
/update
```

## Behavior

1. **Check** if a Context Document exists in the current conversation.
   - If none exists, respond:
     ```
     No Context Document in this session. Run /context or /context fast first.
     ```
2. **Ask** what to update:
   ```
   What would you like to update?
     1) Add new module/feature
     2) Change current work context
     3) Add notes/caveats
     4) Free-form input
   ```
3. After selection, **modify only the relevant section** and re-output the full document.
4. **Remove tags** from updated items and mark them as confirmed.
5. After output, remind:
   ```
   /save [path] — save to file  |  /show — review document
   ```
