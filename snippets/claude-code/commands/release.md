---
description: Merge dev to main after quality gates pass
---

Release verified changes from dev to main branch.

## Prerequisites

- All changes committed to dev
- Quality gates passing (tests, lint, build)
- No pending PRs that should be included

## Steps

1. **Verify dev is clean**:
   ```bash
   git checkout dev
   git status
   git pull origin dev
   ```

2. **Run quality gates**:
   ```bash
   # Run tests (adjust for your project)
   npm test  # or cargo test, pytest, etc.

   # Run linter
   npm run lint  # or cargo clippy, ruff, etc.

   # Run build
   npm run build  # or cargo build, etc.
   ```

3. **Switch to main**:
   ```bash
   git checkout main
   git pull origin main
   ```

4. **Merge dev** (no fast-forward for clear history):
   ```bash
   git merge dev --no-ff -m "release: merge dev to main

   Co-Authored-By: Claude <noreply@anthropic.com>"
   ```

5. **Push main**:
   ```bash
   git push origin main
   ```

6. **Optional: Tag release**:
   ```bash
   git tag -a v1.x.x -m "Release v1.x.x"
   git push origin v1.x.x
   ```

7. **Return to dev**:
   ```bash
   git checkout dev
   ```

## Rules

- NEVER release with failing tests
- NEVER force push main
- Always use --no-ff for merge commits
- Tag significant releases

## Rollback

If release has issues:
```bash
git checkout main
git revert -m 1 <merge-commit>
git push origin main
```

## Notes

- This command assumes a main+dev branch workflow
- For simpler workflows, this command may not be needed
- Consider automating quality gates with CI
