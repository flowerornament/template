# Prohibitive Patterns

Use these patterns to define **anti-patterns** - things the agent should never do.

## Structure

```markdown
## Anti-Patterns

- Never [dangerous action]
- Do not [common mistake]
- Avoid [suboptimal approach]
```

## Examples

### Git Safety
```markdown
## Anti-Patterns

- Never force push to shared branches
- Never commit secrets, API keys, or credentials
- Never skip pre-commit hooks without explicit permission
- Never amend commits that have been pushed
- Never push to main/master without explicit permission
```

### Code Changes
```markdown
## Anti-Patterns

- Never delete files without explicit confirmation
- Never make changes to files you haven't read
- Never modify code outside the scope of the current task
- Never introduce dependencies without discussion
```

### Security
```markdown
## Anti-Patterns

- Never log sensitive data (passwords, tokens, PII)
- Never disable security checks to "make it work"
- Never expose internal APIs publicly
- Never store secrets in code or config files
```

### Communication
```markdown
## Anti-Patterns

- Never assume requirements - ask when unclear
- Never make large changes without explaining the plan
- Never ignore error messages or warnings
- Never proceed if tests are failing
```

## Tips

1. **Start with "Never" or "Do not"** - Clear prohibition language
2. **Explain the risk** - Why is this dangerous?
3. **Focus on irreversible actions** - Prioritize high-consequence mistakes
4. **Keep the list short** - Long prohibition lists feel restrictive

## Severity Levels

Consider categorizing by severity:

```markdown
## Critical (data loss / security risk)
- Never commit secrets to version control
- Never delete production data

## Important (workflow / quality impact)
- Never skip tests before merging
- Never force push to shared branches

## Preferred (style / consistency)
- Avoid deeply nested conditionals
- Avoid magic numbers without constants
```
