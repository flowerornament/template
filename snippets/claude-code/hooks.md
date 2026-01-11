# Claude Code Hooks Configuration

Hooks allow Claude Code to run commands automatically at specific points in the workflow.

## Recommended Hooks

Add to `.claude/settings.local.json`:

```json
{
  "hooks": {
    "SessionStart": [
      {
        "type": "command",
        "command": "bd prime"
      }
    ],
    "PreCompact": [
      {
        "type": "command",
        "command": "bd prime"
      }
    ]
  }
}
```

## Hook Types

### SessionStart

Runs when Claude Code starts a new session.

**Recommended**: `bd prime` - Loads beads workflow context into the conversation.

### PreCompact

Runs before context compaction (when context window fills up).

**Recommended**: `bd prime` - Re-injects beads context after compaction.

### PostToolExecution

Runs after each tool execution.

**Use case**: Custom logging or validation.

## Setup Instructions

1. Create `.claude/settings.local.json` if it doesn't exist
2. Add the hooks configuration above
3. Verify with a fresh session

## Beads Prime Output

When `bd prime` runs, it injects:
- Available commands (bd ready, bd show, etc.)
- Current issue states
- Session close protocol reminders
- Workflow guidelines

## Custom Hooks

You can add custom hooks for project-specific needs:

```json
{
  "hooks": {
    "SessionStart": [
      { "type": "command", "command": "bd prime" },
      { "type": "command", "command": "echo 'Custom startup'" }
    ]
  }
}
```

## Troubleshooting

### Hooks not running

1. Check `.claude/settings.local.json` exists
2. Verify JSON syntax is valid
3. Ensure commands are in PATH

### bd prime fails

1. Verify beads is installed: `which bd`
2. Check .beads/ directory exists
3. Run `bd doctor` to diagnose

## Notes

- Hooks run synchronously
- Failed hooks show warnings but don't block
- Use `settings.local.json` for machine-specific hooks
- Use `settings.json` for shared team hooks
