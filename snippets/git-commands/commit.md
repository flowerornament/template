---
description: Sync bd, stage all changes, commit with good message, push
---

Commit and push all outstanding changes.

## Steps

1. Run `bd sync` to capture any task changes (if using beads)
2. Run `git status` to see what's changed
3. Run `git diff --stat` to understand scope

### Commit

4. Stage all changes: `git add -A`
5. Write a commit message:
   - First line: 50 chars max, summarizes the "what"
   - Use conventional prefixes: feat/fix/chore/docs/refactor
   - Reference task IDs if relevant (e.g., "feat(task-123): add feature")
6. Commit (never --amend unless explicitly told)
7. Push: `git push`

## Rules

- NEVER force push
- NEVER amend commits that have been pushed
- If commit fails (hooks), fix and create NEW commit
- End message with: Generated with [Agent Name]

## Message Format

```
type(scope): short description

Longer explanation if needed.

Generated with [Agent Name]
```

Types: feat, fix, chore, docs, refactor, test, style
