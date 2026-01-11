# Example Project Templates

Working examples of project setups for different archetypes.

## Archetypes

| Example | Use Case | Key Features |
|---------|----------|--------------|
| `build/` | New feature or app development | GSD planning, dev branch, full CLAUDE.md |
| `research/` | Investigation, no code output | Beads, research notes structure |
| `automate/` | Agent-managed system | Beads, execution logs, scheduled tasks |

## How to Use

1. Choose the archetype that matches your project
2. Copy the example directory to your new project
3. Customize the CLAUDE.md and other files for your needs
4. Initialize git and beads if included

```bash
# Example: starting a new build project
cp -r examples/build/ ~/code/my-new-project/
cd ~/code/my-new-project
git init
# Customize CLAUDE.md for your project
```

## What's in Each Example

### build/
- `CLAUDE.md` - Full development instructions
- `.claude/` - Commands and hooks
- `.planning/` - GSD planning structure
- `.gitignore` - Common patterns

### research/
- `CLAUDE.md` - Research-focused instructions
- `.ai/research/` - Questions, findings, sources
- `.beads/` - Track research tasks
- `.gitignore` - Common patterns

### automate/
- `CLAUDE.md` - Automation instructions
- `.ai/automation/` - Schedule, triggers, outputs
- `.beads/` - Track issues
- `logs/` - Execution history
- `.gitignore` - Common patterns
