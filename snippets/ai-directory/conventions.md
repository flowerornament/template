# Code Conventions

## General

- Prefer clarity over cleverness
- Keep functions focused and small
- Name things descriptively

## Language-Specific

### [Language 1]

```
# Style examples
```

### [Language 2]

```
# Style examples
```

## File Organization

- One concept per file where practical
- Group related functionality
- Keep test files adjacent to source

## Naming

| Type | Convention | Example |
|------|------------|---------|
| Files | kebab-case | `my-component.ts` |
| Functions | camelCase | `processInput()` |
| Constants | UPPER_SNAKE | `MAX_RETRIES` |

## Error Handling

- Prefer explicit error returns over exceptions
- Log at appropriate levels
- Provide actionable error messages

## Testing

- Test behavior, not implementation
- One assertion per test when practical
- Use descriptive test names

## Anti-Patterns

Things to avoid in this codebase:
- Pattern 1: Why it's problematic
- Pattern 2: What to do instead
