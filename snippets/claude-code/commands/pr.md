---
description: Create a pull request for current changes
---

Create a PR for significant changes that need review.

## Steps

1. **Ensure changes are committed**:
   ```bash
   git status
   ```
   If uncommitted changes exist, run /commit first.

2. **Sync beads** (if using):
   ```bash
   bd sync
   ```

3. **Check current branch**:
   ```bash
   git branch --show-current
   ```

### If on main/master (create feature branch)

4. **Create feature branch**:
   ```bash
   git checkout -b feat/<description>
   ```

5. **Push with upstream**:
   ```bash
   git push -u origin feat/<description>
   ```

### Create PR

6. **Use gh CLI**:
   ```bash
   gh pr create --title "<title>" --body "$(cat <<'EOF'
   ## Summary
   <1-3 bullet points of what this PR does>

   ## Changes
   - Change 1
   - Change 2

   ## Test Plan
   - [ ] Test 1
   - [ ] Test 2

   Co-Authored-By: Claude <noreply@anthropic.com>
   EOF
   )"
   ```

7. **Report PR URL** to user

## Rules

- PR title should be clear and concise
- Include test plan in description
- Link related issues if applicable
- Request review if team project

## Branch Naming

- `feat/<description>` - New features
- `fix/<description>` - Bug fixes
- `chore/<description>` - Maintenance
- `docs/<description>` - Documentation

## Example

```bash
git checkout -b feat/add-dark-mode
git push -u origin feat/add-dark-mode
gh pr create --title "feat: add dark mode toggle" --body "..."
```
