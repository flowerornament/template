# Content Pattern Templates

Templates for writing effective agent instructions in CLAUDE.md and other agent documentation.

## Pattern Types

### Prescriptive (do this)
Clear directives about required practices.

### Prohibitive (don't do this)
Explicit boundaries and anti-patterns to avoid.

### Conditional (if/then)
Decision rules for context-dependent behavior.

### Explanatory (why)
Context and reasoning for agent understanding.

## Best Practices

1. **Be specific** - Vague instructions lead to inconsistent behavior
2. **Prioritize** - Important rules should come first
3. **Give examples** - Show, don't just tell
4. **Explain context** - Help agents understand when rules apply
5. **Keep it scannable** - Agents process in chunks, not walls of text

## Combining Patterns

Effective agent documentation typically combines patterns:

```markdown
## Git Workflow

### Required Practices
- Run tests before committing
- Use conventional commit prefixes (feat/fix/chore)
- Include meaningful commit messages

### Anti-Patterns
- Never force push to main
- Never skip pre-commit hooks
- Never commit secrets

### Decision Rules
- If changing >10 files: create PR instead of direct commit
- If tests fail: do not commit, fix first
- If uncertain: ask before proceeding

### Context
This project uses a trunk-based workflow with short-lived branches.
Direct commits to dev are allowed for small changes.
```
