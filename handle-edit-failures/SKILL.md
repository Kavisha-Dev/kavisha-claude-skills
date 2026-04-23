---
name: handle-edit-failures
description: When a file edit (search_replace, patch, or write) fails once, stop retrying. Give the user the exact content and location to apply manually. Use when any edit attempt fails or when the user asks not to retry repeatedly on failed edits.
---

# Handle Edit Failures

## Rule

If a file edit fails **once** (e.g. `search_replace` reports "old_string not found" or similar), **stop**. Do not:

- Retry with relaxed matching, different whitespace, or alternate strategies
- Run shell/Python scripts to perform the edit
- Try the same edit in multiple ways

## What to Do Instead

1. **Stop after the first failure** for that edit.
2. **Tell the user** that the edit could not be applied automatically.
3. **Provide exact content** they can add or replace:
   - The **file path**
   - The **exact text** to insert or the **exact replacement** (in a fenced block if helpful)
   - The **location**: e.g. "after line 44", "replace lines 10–15 with", or "before the line containing `...`"
4. **Continue** with any remaining tasks; do not block the rest of the work on this one edit.

## Example Output (when an edit fails)

```text
The edit failed. Add the following manually in `path/to/file.md`:

**Location:** After the line containing `deleted_sample_gratitudes_global` (before the App Group section).

**Insert these lines:**

|| `glv.notifications.hasPrompted` | Bool | Whether the pre-prompt... | No | Yes |
|| `glv.notifications.isEnabled` | Bool | Whether the user granted... | No | Yes |
|| `glv.notifications.limitCardSeenCount` | Int | How many times... | No | Yes |

Then continue with the remaining tasks.
```

## Scope

Applies to **any** file type (source, config, markdown, plist, etc.). The same rule holds regardless of whether the failure is due to special characters, encoding, table formatting, or fuzzy match issues.
