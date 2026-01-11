---
description: Stage all changes, commit with good message, push
---

Commit and push all outstanding changes.

## Steps

1. **Sync beads** (if using beads):
   ```bash
   bd sync
   ```

2. **Check status**:
   ```bash
   git status
   git diff --stat
   ```

3. **Stage all changes**:
   ```bash
   git add -A
   ```

4. **Commit with conventional message**:
   - First line: 50 chars max, summarizes the "what"
   - Use conventional prefixes: feat/fix/chore/docs/refactor/test
   - Reference task IDs if relevant (e.g., "feat(beads-xxx): add feature")
   ```bash
   git commit -m "type(scope): description

   Longer explanation if needed.

   Co-Authored-By: Claude <noreply@anthropic.com>"
   ```

5. **Push to remote**:
   ```bash
   git push
   ```

6. **Verify**:
   ```bash
   git status
   ```

## Rules

- NEVER force push
- NEVER amend commits that have been pushed
- If hooks reject commit, fix and create NEW commit
- Work is NOT complete until push succeeds

## Message Format

```
type(scope): short description

Longer explanation if needed.

Co-Authored-By: Claude <noreply@anthropic.com>
```

**Types**: feat, fix, chore, docs, refactor, test, style

## Examples

```
feat(auth): add login validation

fix: resolve null pointer in parser

chore: update dependencies

docs: add API documentation

refactor(core): simplify error handling
```
