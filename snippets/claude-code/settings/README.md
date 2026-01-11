# Claude Code Settings Templates

## Files

### settings.json

Shared settings across all users. Typically includes:
- `enabledPlugins` - Plugins to enable for the project

This file can be committed to the repository.

### settings.local.json

Project-specific settings. Includes:
- `permissions.allow` - Pre-approved tool permissions
- `hooks` - Session lifecycle hooks (SessionStart, PreCompact)

This file can be committed but may include user-specific paths.

## Permission Patterns

Claude Code permissions use this syntax:

```
Tool(pattern:*)
```

Examples:
- `Bash(git add:*)` - Allow `git add` with any arguments
- `WebFetch(domain:github.com)` - Allow fetching from github.com
- `WebSearch` - Allow web search

## Hooks

Hooks run at specific lifecycle points:

- **SessionStart** - Runs when a new conversation starts
- **PreCompact** - Runs before conversation compaction/summarization

Common hook patterns:
```json
{
  "hooks": {
    "SessionStart": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "bd prime"
          }
        ]
      }
    ]
  }
}
```

## Usage

1. Copy these files to `.claude/` in your project
2. Customize permissions for your workflow
3. Add project-specific hooks as needed
4. Commit `settings.json`, optionally `settings.local.json`
