---
description: Quick WIP commit without push
---

Create a work-in-progress commit for saving state without pushing.

## Steps

1. **Check status**:
   ```bash
   git status
   ```

2. **Stage all changes**:
   ```bash
   git add -A
   ```

3. **Commit with WIP prefix**:
   ```bash
   git commit -m "WIP: <brief description of current state>

   Co-Authored-By: Claude <noreply@anthropic.com>"
   ```

## When to Use

- End of session, work incomplete
- Before switching contexts
- Checkpoint before risky changes
- Need to save state but not ready to push

## Notes

- WIP commits can be squashed later
- Don't push WIP commits to shared branches
- Include enough description to resume later
- Consider `git stash` for very temporary saves

## Cleaning Up WIP Commits

Before pushing, squash WIP commits:
```bash
# Interactive rebase to squash
git rebase -i HEAD~<n>
# Mark WIP commits as 'squash' or 'fixup'
```

Or reset and recommit:
```bash
git reset --soft HEAD~<n>
git commit -m "feat: complete description"
```

## Examples

```
WIP: halfway through auth refactor
WIP: tests passing, need error handling
WIP: UI mostly done, need styling
```
