---
description: Sync beads issue state with git remote
---

Sync beads tracking data with the remote repository.

## Steps

1. **Check sync status**:
   ```bash
   bd sync --status
   ```

2. **Sync with remote**:
   ```bash
   bd sync
   ```

3. **Verify sync**:
   ```bash
   bd sync --status
   ```

## When to Use

- Before ending a session
- After creating/closing multiple issues
- Before switching branches
- After pulling changes from remote

## What Gets Synced

- Issue state changes (open → in_progress → closed)
- New issues created locally
- Issues created by collaborators
- Dependency updates

## Troubleshooting

### Sync conflicts

If sync fails due to conflicts:
```bash
bd sync --force  # Use with caution
```

### Missing beads-sync branch

If the beads-sync branch doesn't exist:
```bash
git checkout --orphan beads-sync
git rm -rf .
git add .beads/
git commit -m "Initialize beads tracking"
git push -u origin beads-sync
git checkout main  # or dev
```

### Check beads health

```bash
bd doctor
```

## Notes

- Sync is automatically called by hooks on session start
- Always sync before push to ensure issue state is captured
- The beads-sync branch keeps issue data separate from code
