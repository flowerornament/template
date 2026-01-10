# {{PROJECT_NAME}}

{{PROJECT_DESCRIPTION}}

## Task Tracking

This project uses **bd** (beads) for issue tracking.

```bash
bd ready              # Find available work
bd show <id>          # View issue details
bd update <id> --status in_progress  # Claim work
bd close <id>         # Complete work
bd sync --from-main   # Pull beads updates (ephemeral branches)
```

## Workflow

### Starting a Session
```bash
bd prime              # Load context after compaction/new session
bd ready              # See what's available
```

### Creating Issues
```bash
bd create --title="..." --type=task --priority=2
# Priority: 0-4 (0=critical, 2=medium, 4=backlog)
# Types: task, bug, feature, epic
```

### Session End Checklist
```
[ ] git status                 (check changes)
[ ] git add <files>            (stage code)
[ ] bd sync --from-main        (pull beads updates)
[ ] git commit -m "..."        (commit)
```

## Build/Run

```bash
# Project-specific commands here
```

## Structure

Key directories and files.
