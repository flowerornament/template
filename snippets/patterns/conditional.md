# Conditional Patterns

Use these patterns to define **decision rules** - context-dependent behaviors.

## Structure

```markdown
## Decision Rules

- If [condition], then [action]
- When [trigger], [response]
- [Condition] requires [special handling]
```

## Examples

### Code Review Thresholds
```markdown
## Decision Rules

- If changing >10 files: create PR instead of direct commit
- If touching core modules: add extra test coverage
- If modifying public API: update documentation
- If tests fail: do not commit, fix first
```

### Branching Strategy
```markdown
## Decision Rules

- If on main branch: create feature branch before changes
- If small fix (<10 lines): commit directly to dev
- If large feature: create PR and request review
- If hotfix needed: branch from main, merge back to both
```

### Error Handling
```markdown
## Decision Rules

- If API returns 401: prompt for new credentials
- If API returns 429: implement exponential backoff
- If file not found: check alternate locations before erroring
- If dependency conflict: report and ask for guidance
```

### Communication
```markdown
## Decision Rules

- If task will take >5 minutes: provide progress updates
- If requirements unclear: ask before proceeding
- If multiple approaches possible: present options with tradeoffs
- If encountering unexpected state: pause and explain
```

### File Operations
```markdown
## Decision Rules

- If file is large (>1000 lines): read in chunks
- If file is binary: skip, note in response
- If file contains secrets: redact in output
- If path doesn't exist: create parent directories
```

## Tips

1. **Clear conditions** - Measurable thresholds when possible
2. **Explicit actions** - What exactly should happen?
3. **Cover edge cases** - What if none of the conditions match?
4. **Order matters** - First matching rule wins (usually)

## Advanced: Decision Trees

For complex logic, use nested conditions:

```markdown
## Commit Strategy

```
Is this a fix for a regression?
├─ Yes → Commit directly to dev
└─ No → Check change size
         ├─ <10 files, <100 lines → Commit directly
         └─ Otherwise → Create PR
```
```

## Default Behaviors

Always define what happens when no rule matches:

```markdown
## Decision Rules

- If changing configuration: require confirmation
- If adding new dependency: document reason
- **Default**: proceed with standard workflow
```
