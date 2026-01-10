# {{PROJECT_NAME}} - Agent Instructions

## Overview

{{PROJECT_DESCRIPTION}}

## Task Tracking

This project uses **bd** (beads) for issue tracking.

### Core Commands
```bash
bd prime              # Start session, get context
bd ready              # Find available work (no blockers)
bd show <id>          # View issue details
bd update <id> --status in_progress  # Claim work
bd close <id>         # Complete work
bd sync               # Sync to beads-sync branch
```

### Creating Issues
```bash
bd create --title="..." --type=task|bug|feature --priority=2
bd dep add <issue> <blocker>  # Add dependency
```

Priority scale: 0=critical, 1=high, 2=medium, 3=low, 4=backlog

## Git Workflow

### Branches
- `main` - Stable, deployable code
- `dev` - Integration branch for in-progress work
- `beads-sync` - Issue tracking state (auto-managed)
- `feature/*` - Feature branches for PRs

### Commit Flow
1. Work on `dev` or feature branch
2. `/commit` - Sync bd, stage, commit, push to dev
3. `/pr` - Create PR when ready for main
4. `/release` - Fast-forward main from verified dev

### Rules
- Never force push
- Never amend pushed commits
- Always run `bd sync` before committing
- Push submodules before parent repo

## Documentation

### Architecture
See `.ai/architecture.md` for system design.

### Conventions
See `.ai/conventions.md` for code standards.

### Decisions
ADRs in `.ai/decisions/NNN-title.md`

## Session Completion Checklist

Before ending a session:
```
[ ] File issues for remaining work
[ ] Run quality gates (tests, lint, build)
[ ] Update issue status (close completed, note blockers)
[ ] /commit (or /pr if significant)
[ ] Verify: git log shows your commits
[ ] Handoff context for next session
```

## Quick Reference

| Task | Command |
|------|---------|
| Find work | `bd ready` |
| Claim work | `bd update <id> --status in_progress` |
| Complete | `bd close <id>` |
| Commit | `/commit` |
| Create PR | `/pr` |
| Project stats | `bd stats` |
