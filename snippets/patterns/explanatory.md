# Explanatory Patterns

Use these patterns to provide **context and reasoning** - help agents understand why.

## Structure

```markdown
## Context

[Background information]
[Architectural decisions]
[Historical reasons]
```

## Examples

### Project Architecture
```markdown
## Context

This project uses a modular monorepo structure:
- `/packages/core` - Shared utilities and types
- `/packages/api` - REST API server
- `/packages/web` - React frontend

All packages share a single `node_modules` at the root.
Cross-package imports use workspace references.
```

### Workflow Rationale
```markdown
## Context

We use the beads-sync branch because multiple Claude instances
may work in parallel, and we need issue state isolated from code
changes. This prevents merge conflicts when tracking work.

The SessionStart hook runs `bd prime` to load issue context
at the beginning of each conversation.
```

### Technical Decisions
```markdown
## Context

This codebase uses TypeScript strict mode. The original JavaScript
was gradually migrated, so some files have `// @ts-check` comments
from the transition period. New code should be TypeScript-first.

We chose Zod for validation over io-ts because the team found
the API more intuitive and the error messages clearer.
```

### Constraints
```markdown
## Context

The production environment runs on AWS Lambda with a 15-minute
timeout and 10GB memory limit. Long-running operations must be
chunked or moved to a separate ECS task.

Cold starts add 2-5 seconds of latency. The API uses provisioned
concurrency for latency-sensitive endpoints.
```

## Tips

1. **Answer "why"** - Don't just state facts, explain reasoning
2. **Be concise** - Enough context to inform decisions
3. **Update when things change** - Stale context misleads
4. **Separate from rules** - Context informs, rules direct

## Combining with Rules

Context makes rules clearer:

```markdown
## Git Workflow

### Context
This project uses trunk-based development with dev as the integration
branch. We avoid long-lived feature branches because they caused
painful merge conflicts in the past.

### Required Practices
- Commit to dev directly for small changes
- Create short-lived branches (< 1 day) for features
- Merge PRs same-day when approved
```

## Project State Context

Help agents understand current state:

```markdown
## Current State

**Active milestone:** v2.0 Performance Improvements
**Current phase:** Database optimization
**Blocked on:** Waiting for staging environment access

Recent changes:
- Migrated from MongoDB to PostgreSQL (last week)
- Added connection pooling (yesterday)
- Performance tests show 3x improvement on reads
```
