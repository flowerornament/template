---
description: Quick WIP commit without push
---

Create a work-in-progress commit for saving state without pushing.

## Steps

1. Run `git status` to see changes
2. Stage all: `git add -A`
3. Commit with WIP prefix:
```bash
git commit -m "WIP: <brief description of state>"
```

## When to Use

- End of session, work incomplete
- Before switching contexts
- Checkpoint before risky changes

## Notes

- WIP commits can be squashed later
- Don't push WIP commits to shared branches
- Include enough description to resume later
