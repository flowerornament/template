# Prescriptive Patterns

Use these patterns to define **required practices** - things the agent should always do.

## Structure

```markdown
## Required Practices

- Always [specific action]
- Before [trigger], ensure [condition]
- When [situation], use [approach]
```

## Examples

### Git Workflow
```markdown
## Required Practices

- Run tests before committing
- Use conventional commit prefixes (feat/fix/chore/docs)
- Include Co-Authored-By line in commits
- Stage changes explicitly (no `git add .` for large changesets)
```

### Code Quality
```markdown
## Required Practices

- Write tests for new functionality
- Document public APIs with JSDoc/docstrings
- Run linter before committing
- Keep functions under 50 lines
```

### Communication
```markdown
## Required Practices

- Summarize what you're about to do before starting
- Report progress on long-running tasks
- Ask for clarification when requirements are ambiguous
- Explain significant decisions with rationale
```

### File Operations
```markdown
## Required Practices

- Read files before editing (never edit blind)
- Create backups before destructive operations
- Verify file existence before assuming paths
- Use absolute paths in scripts and configs
```

## Tips

1. **Start with action verbs** - "Run", "Write", "Include", "Ensure"
2. **Be specific** - "Run tests" is better than "verify code works"
3. **Limit to ~5-7 items** - Too many rules get ignored
4. **Order by importance** - Most critical practices first
