---
name: show
description: |
  Print the current Context Document to the conversation.
  Triggered by "/show" command.
  Use after generating a Context Document with /context or /context fast.
---

# Show Context Document

Print the current Context Document to the conversation for review.

## Usage

```
/show
```

## Behavior

1. **Check** if a Context Document exists in the current conversation.
   - If none exists, respond:
     ```
     No Context Document in this session. Run /context or /context fast first.
     ```
2. **Print** the full Context Document as a markdown code block.
3. After printing, remind available next actions:
   ```
   /update — modify sections  |  /save [path] — save to file
   ```
