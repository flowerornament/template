---
description: Create a pull request for the current changes
---

Create a PR for significant changes that need review.

## Steps

1. Ensure all changes are committed
2. Run `bd sync` if using beads
3. Check current branch: `git branch --show-current`

### If on main/master (create feature branch)

4. Create feature branch: `git checkout -b feat/<description>`
5. Push with upstream: `git push -u origin feat/<description>`

### Create PR

6. Use gh CLI:
```bash
gh pr create --title "<title>" --body "$(cat <<'EOF'
## Summary
<what this PR does>

## Changes
- Change 1
- Change 2

## Test Plan
- [ ] Test 1
- [ ] Test 2

Generated with [Agent Name]
EOF
)"
```

7. Report the PR URL to the user

## Rules

- PR title should be clear and concise
- Include test plan in description
- Link related issues if applicable
- Request review if team project
