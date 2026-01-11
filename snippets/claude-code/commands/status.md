---
description: Show git status and beads issue status
---

Display current state of repository and tracked work.

## Steps

1. **Git status**:
   ```bash
   git status
   ```

2. **Branch info**:
   ```bash
   git branch -vv
   ```

3. **Recent commits**:
   ```bash
   git log --oneline -5
   ```

4. **Beads status** (if using):
   ```bash
   bd list --status=in_progress
   bd ready
   ```

5. **Sync status** (if using beads):
   ```bash
   bd sync --status
   ```

## Output Summary

Report to user:
- Current branch and tracking status
- Uncommitted changes (if any)
- Recent commits
- In-progress tasks (if using beads)
- Ready tasks (if using beads)
- Sync status with remote

## Example Output

```
Branch: dev (tracking origin/dev, up to date)
Uncommitted: 3 files modified

Recent commits:
- abc1234 feat: add feature X
- def5678 fix: resolve bug Y

In Progress:
- beads-abc: Implement feature X

Ready to work:
- beads-def: Add tests for feature X
- beads-ghi: Update documentation

Beads sync: up to date with remote
```
