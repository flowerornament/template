# {{PROJECT_NAME}}

{{PROJECT_DESCRIPTION}}

## Purpose

This is an **automation project** - an agent-managed system that runs on a schedule or in response to triggers.

## Task Tracking

This project uses **bd** (beads) for tracking issues and improvements.

### Quick Reference
```bash
bd ready              # See available tasks
bd show <id>          # View task details
bd create --title="<description>" --type=bug|task|feature
bd update <id> --status=in_progress
bd close <id>         # Mark complete
bd sync               # Sync with remote
```

## Project Structure

```
{{PROJECT_NAME}}/
├── CLAUDE.md         # This file
├── .ai/
│   ├── schedule.md   # When this runs
│   ├── triggers.md   # What triggers execution
│   └── outputs.md    # What gets produced
├── config/           # Runtime configuration
├── logs/             # Execution history
├── src/              # Source code (if any)
└── .beads/           # Issue tracking
```

## Automation Context

### Schedule
See `.ai/schedule.md` for when this runs.

### Triggers
See `.ai/triggers.md` for what triggers execution.

### Outputs
See `.ai/outputs.md` for what this produces.

## Execution Guidelines

- **Idempotency**: Operations should be safe to re-run
- **Logging**: All executions should be logged to `logs/`
- **Error handling**: Failures should be captured and reported
- **Configuration**: Runtime settings go in `config/`

## Development vs Production

When modifying this automation:
1. Test changes locally first
2. Review logs from recent executions
3. Update schedule/triggers/outputs docs if behavior changes
4. Consider rollback strategy

## Session End

Before ending any session:
1. Document any changes to automation behavior
2. Update .ai/ docs if schedule/triggers/outputs changed
3. Close completed tasks: `bd close <id>`
4. Sync task state: `bd sync`
5. Push changes: `git push`
